<template>
  <swiper
    :slidesPerView="getImageCount"
    :spaceBetween="getBetween"
    :modules="modules"
    :observer="true"
    :observeParents="true"
    :parallax="true"
    ref="swiper"
    class="bg-none pr-5 pl-5 py-5"
  >
    <swiper-slide
      v-for="(item, index) in LiveEvents"
      :key="index"
      class="item no-border bg-none subscription-item"
    >
      <div class="d-flex flex-column w-100 live-event">
        <div
          style="display: relative"
          @click="onClickLiveTV(item.live_event_id)"
        >
          <img
            :src="isDev ? CardLive : item.live_event_image_wide"
            class="card-top-img event-vod-img"
          />
          <div v-if="!item.package_status" :class="disabled_vod">
            <img :src="LockImage" style="width: 100px; height: 100px" />
          </div>
        </div>

        <div class="d-flex justify-start align-center live-event-content">
          <v-avatar size="40" class="avatar-img ml-3">
            <img
              :src="item.content_provider_logo"
              style="width: 40px; height: 40px; border-radius: 50%"
              @click="onClickProvider(item.content_provider_id)"
            />
          </v-avatar>
          <div
            class="d-flex flex-column text-left mb-3"
            style="width: 100%"
            @click="onClickLiveTV(item.live_event_id)"
          >
            <div class="d-flex justify-space-between mt-3  ml-5">
              <div
                class="d-flex flex-column fm fcw event_short_name justify-center short_name"
                style="max-width: 300px; height: 60px; font-size: 14px"
              >
                <p class="text-truncate">{{ item.live_event_name_short }}</p>
                <p class="text-truncate">{{ item.content_provider_name }}</p>
              </div>
              <v-img
                v-if="item.channel_status == 'ACTIVE'"
                :src="LiveStatus"
                width="56"
                height="25"
                class="ml-10"
                style="float: right"
              >
              </v-img>
            </div>

            <h3
              class="fm fcg ml-5 text-truncate date-size"
              style="max-width: 17vw; font-size: 14px; font-weight: 100"
            >
              {{ item.live_event_date }}
              <!-- 13th Feb 2024 - 08:00 pm -->
            </h3>
          </div>
        </div>
      </div>
    </swiper-slide>
    <template v-slot:button-prev>
      <div
        @click="$refs.swiper.swiperInstance.slidePrev()"
        class="swiper-top-position swiper-button-prev"
      ></div>
    </template>
    <template v-slot:button-next> </template>
  </swiper>
</template>

<style scoped lang="scss">
  @import '../styles/home.scss';
</style>

<script>
  import CardLive from '../assets/img/card-live.png'
  import LiveLogo from '../assets/img/icon-live-logo-blue.png'
  import LiveStatus from '../assets/img/live-status.png'
  import VideoPlayer from '@/components/VodeoPlayer.vue'
  import LockImage from '../assets/img/lock.svg'
  import { changeTimeFormatEST } from '../utils/date'
  import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
  import 'swiper/swiper-bundle.min.css'
  import { devMode } from '../utils/devConfig'

  // import required modules
  import { Pagination, Keyboard, Navigation, Scrollbar, A11y } from 'swiper'
  import { number } from '@intlify/core-base'

  export default {
    components: {
      Swiper,
      SwiperSlide,
      VideoPlayer,
    },
    props: {
      categoryId: {
        type: number,
        required: true,
      },
    },
    data() {
      return {
        LiveLogo: LiveLogo,
        LiveStatus: LiveStatus,
        CardLive: CardLive,
        CategoryData: this.categoryId,
        LockImage: LockImage,
        ttt: [],
        isDev: devMode,
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev',
        },
        disabled_vod: 'disabled-event-vod',
        image_count: 4,
        between: 15,
      }
    },
    mounted() {},
    methods: {
      getLiveEvents() {
        this.$store.dispatch('setLiveEventsByCategoryId', {
          CategoryId: this.categoryId,
        })
      },
      onClickLiveTV(id) {
        this.$router.push({ path: '/event/player/' + id })
      },
      onClickProvider(id) {
        this.$router.push({ path: '/provider/' + id })
      },
    },
    computed: {
      LiveEvents() {
        let resultVal = []
        let val = []
        if (this.$store.state.EventsStore.Events.length == 0) {
          this.getLiveEvents()
        }
        val = this.$store.state.EventsStore.Events[this.categoryId]
        if (val != null && val.length > 0) {
          val.map((item) => {
            item.live_event_date = changeTimeFormatEST(item.live_event_date)
            resultVal.push(item)
          })
        }
        this.ttt = resultVal
        return resultVal
      },
      getImageCount() {
        let width = window.innerWidth

        if (width > 572) {
          this.image_count = 4
        } else {
          this.image_count = 1.3
        }
        return this.image_count
      },
      getBetween() {
        let width = window.innerWidth
        if (width > 572) {
          this.between = 15
        } else {
          this.between = 10
        }
        return this.between
      },
    },
    watch: {
      LiveEvents(newVal) {
        return newVal
      },
      categoryId(newVal) {
        return newVal
      },
    },
    setup() {
      return {
        modules: [Pagination, Keyboard, Navigation, Scrollbar, A11y],
      }
    },
  }
</script>

<style>
  .active-event-vod {
    opacity: 1;
  }

  .disabled-event-vod {
    background: rgb(17 17 17);
    position: absolute !important;
    left: 0;
    right: 0;
    bottom: 102px;
    top: 0;
    z-index: 1001;
    margin: 0;
    opacity: 0.5 !important;
    align-items: center;
    justify-content: center;
    display: flex !important;
  }

  .event-vod-img {
    width: 441px;
    height: 249px;
    border-radius: 1vw;
  }

  @media screen and (min-width: 1279px) and (max-width: 1535px) {
    .event-vod-img {
      width: 255px !important;
      height: 143px !important;
      border-radius: 1vw;
    }

    .event_short_name {
      max-width: 190px !important;
    }
  }

  @media screen and (max-width: 600px) {
    .event-vod-img {
      max-width: 100% !important;
      height: auto !important;
      border-top-left-radius: 2vw !important;
      border-top-right-radius: 2vw !important;
      border-bottom-left-radius: 0 !important;
      border-bottom-right-radius: 0 !important;
    }

    .event_short_name {
      max-width: 200px !important;
    }
    .short_name {
      font-size: 16px !important;
    }
    .date-size {
      font-size: 16px !important;
      max-width: 350px !important;
    }

    .live-event-content{
      background-color: lightgray;
      border-bottom-left-radius: 2vw !important;
      border-bottom-right-radius: 2vw !important;
    }
  }

  @media screen and (min-width: 1536px) and (max-width: 1699px) {
    .event-vod-img {
      width: 320px !important;
      height: 180px !important;
      border-radius: 1vw;
    }

    .event_short_name {
      max-width: 255px !important;
    }
  }

  @media screen and (min-width: 1700px) and (max-width: 1999px) {
    .event-vod-img {
      width: 365px !important;
      height: 205px !important;
      border-radius: 1vw;
    }
    .event_short_name {
      height: 60px;
    }
  }

  @media screen and (min-width: 2000px) and (max-width: 2150px) {
    .event-vod-img {
      width: 435px !important;
      height: 245px !important;
      border-radius: 1vw;
    }
    .event_short_name {
      max-width: 365px !important;
    }
  }

  @media screen and (min-width: 2151px) and (max-width: 2400px) {
    .event-vod-img {
      width: 490px !important;
      height: 275px !important;
      border-radius: 1vw;
    }
    .event_short_name {
      max-width: 425px !important;
    }
  }

  @media screen and (min-width: 2401px) and (max-width: 2560px) {
    .event-vod-img {
      width: 510px !important;
      height: 287px !important;
      border-radius: 1vw;
    }
    .event_short_name {
      max-width: 440px !important;
    }
  }

  @media screen and (min-width: 2561px) and (max-width: 2880px) {
    .event-vod-img {
      width: 575px !important;
      height: 324px !important;
      border-radius: 1vw;
    }
    .event_short_name {
      max-width: 440px !important;
    }
  }

  @media screen and (min-width: 2881px) {
    .event-vod-img {
      width: 820px !important;
      height: 461px !important;
      border-radius: 1vw;
    }
  }
</style>
