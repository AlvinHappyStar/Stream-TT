<template>
  <div v-if="this.SliderItems.length > 0">
    <v-carousel
      :show-arrows="false"
      cycle
      show-arrows-on-hover
      style="width: 100vw; height: 56.4vw"
      class="carousel_first"
    >
      <!-- <v-carousel-item v-for="(item, i) in SliderItems" :key="i" :style="{ opacity: opacityLevel }"
                        :src="item.landscapeImage">
                        <div v-if="item.trailer_url != ''">
                            <VideoPlayer :options="{ autoPlay: true, controls: true, sources: [{ src: item.trailer_url }] }" />
                        </div>
                        <v-sheet color="transparent" height="100%" tile>
                            <v-row class="d-flex flex-column fill-height" align="left" justify="center">
                                <v-col cols="5" class="pa-16 ml-10">
                                    <div class="d-flex justify-start align-center mb-2">
                                        <img v-if="item.titleImage" :src="item.titleImage" style="width: 16vw;">
                                        <h4 v-else class="text-h3 font-weight-black">{{ item.title }}</h4>
                                    </div>
                                    <div class="text-subtitle-1 font-weight-medium text-justify mb-2">
                                        {{ item.description }}
                                    </div>
                                    <div class="text-h6 text-left mb-1">
                                        {{ SliderTypeBycontentType(item.contentType) }}
                                    </div>
                                    <div class="text-h6 text-left mb-10">
                                        2022 2H 34M
                                    </div>
                                    <div class="d-flex justify-start align-center">
                                        <v-btn class="d-flex justify-flex-end align-center pr-4"
                                            style="background: hsl(242deg 2% 5%);"
                                            @click="onGoPlayer(item.contentID, item.contentType)">
                                            <v-icon
                                                style="font-size:34px;border-radius:50%;background:darkred;padding:28px;margin-right:12px;margin-left: -24px; z-index: 9999;">
                                                mdi-play
                                            </v-icon>
                                            Play
                                        </v-btn>
                                        <v-btn class="d-flex justify-flex-end align-center pr-4 ml-6"
                                            style="background: hsl(242deg 2% 5%);"
                                            @click="onGoTailer(item.contentID, item.contentType)">
                                            <v-icon
                                                style="font-size:34px;border-radius:50%;background:darkred;padding:28px;margin-right:12px;margin-left: -24px; z-index: 9999;">
                                                mdi-play
                                            </v-icon>
                                            Tailer
                                        </v-btn>
                                    </div>
                                </v-col>
                            </v-row>
                        </v-sheet>
                    </v-carousel-item> -->
      <v-carousel-item
        :style="{ opacity: opacityLevel }"
        v-for="(item, i) in this.SliderItems"
        :key="i"
        :src="item.landscapeImage"
      >
        <!-- <div v-if="item.trailer_url != ''" style="width: 100vw; height:56.4vw;">
                    <VideoPlayer :options="{ autoPlay: true, controls: false, preload: 'auto', loop: true, muted: false, sources: [{ src: item.trailer_url }] }" />
                    <v-sheet color="transparent" height="100%" tile>
                        <v-row class="d-flex flex-column fill-height" align="left" justify="center">
                            <v-col cols="5" class="pa-16 ml-10">
                                <div class="d-flex justify-start align-center mb-2">
                                    <img v-if="item.titleImage" :src="item.titleImage" style="width: 16vw;">
                                    <h4 v-else class="text-h3 font-weight-black">{{ item.title }}</h4>
                                </div>
                                <div class="text-subtitle-1 font-weight-medium text-justify mb-2">
                                    {{ item.description }}
                                </div>
                                <div class="text-h6 text-left mb-1">
                                    {{ SliderTypeBycontentType(item.contentType) }}
                                </div>
                                <div class="text-h6 text-left mb-10">
                                    2022 2H 34M
                                </div>
                                <div class="d-flex justify-start align-center">
                                    <v-btn class="d-flex justify-flex-end align-center pr-4"
                                        style="background: hsl(242deg 2% 5%);"
                                        @click="onGoPlayer(item.contentID, item.contentType)">
                                        <v-icon
                                            style="font-size:34px;border-radius:50%;background:darkred;padding:28px;margin-right:12px;margin-left: -24px; z-index: 9999;">
                                            mdi-play
                                        </v-icon>
                                        Play
                                    </v-btn>
                                    <v-btn class="d-flex justify-flex-end align-center pr-4 ml-6"
                                        style="background: hsl(242deg 2% 5%);"
                                        @click="onGoTailer(item.contentID, item.contentType)">
                                        <v-icon
                                            style="font-size:34px;border-radius:50%;background:darkred;padding:28px;margin-right:12px;margin-left: -24px; z-index: 9999;">
                                            mdi-play
                                        </v-icon>
                                        Tailer
                                    </v-btn>
                                </div>
                            </v-col>
                        </v-row>
                    </v-sheet>
                </div> -->
        <!-- <div v-else style="width: 100vw; height:56.4vw;"> -->
        <v-sheet color="transparent" height="70%">
          <v-row
            class="d-flex flex-column fill-height"
            align="center"
            justify="center"
          >
            <v-col
              cols="12"
              class="mb-3 preview-scene d-flex flex-column align-center align-md-start justify-center"
            >
              <div
                class="d-flex justify-center justify-md-start mb-3 film-title"
              >
                <img
                  v-if="item.titleImage"
                  :src="item.titleImage"
                  style="width: 16vw"
                  class="img-title"
                />
                <h4
                  v-else
                  class="text-h3 font-weight-black text-md-left"
                  id="film_subject"
                >
                  {{ item.title }}
                </h4>
              </div>
              <div
                class="text-subtitle-1 font-weight-medium text-justify mb-2 film-descrip d-none d-md-flex"
                style="line-height: 20px"
              >
                {{ item.description }}
              </div>
              <div
                v-if="item.movieDetail && item.movieDetail.length > 0"
                class="text-subtitle-1 font-weight-medium text-justify mb-2 released-year"
              >
                Released Year:
                {{
                  item.movieDetail.length > 0 ? item.movieDetail[0].year : ''
                }}
              </div>
              <div
                v-if="
                  item.movieDetail &&
                  item.movieDetail.length > 0 &&
                  item.movieDetail[0].duration
                "
                class="text-subtitle-1 font-weight-medium text-justify mb-2 run-time d-none d-md-block"
              >
                Runtime:
                {{
                  item.movieDetail.length > 0
                    ? this.setRuntime(item.movieDetail[0].duration)
                    : '0M'
                }}
              </div>
              <div class="text-h6 text-left mb-3 movie-kind">
                {{ SliderTypeBycontentType(item.contentType) }}
              </div>
              <div class="d-none d-md-flex justify-start align-center play-btn">
                <v-btn
                  class="d-flex justify-flex-end align-center pr-4"
                  style="background: hsl(242deg 2% 5%)"
                  @click="onGoPlayer(item.contentID, item.contentType)"
                >
                  <v-icon
                    style="
                      font-size: 34px;
                      border-radius: 50%;
                      background: darkred;
                      padding: 28px;
                      margin-right: 12px;
                      margin-left: -24px;
                      z-index: 9999;
                    "
                  >
                    mdi-play
                  </v-icon>
                  Play
                </v-btn>
                <!-- <v-btn class="d-flex justify-flex-end align-center pr-4 ml-6"
                                        style="background: hsl(242deg 2% 5%);"
                                        @click="onGoTailer(item.contentID, item.contentType)">
                                        <v-icon
                                            style="font-size:34px;border-radius:50%;background:darkred;padding:28px;margin-right:12px;margin-left: -24px; z-index: 9999;">
                                            mdi-play
                                        </v-icon>
                                        Tailer
                                    </v-btn> -->
              </div>
              <div
                class="d-flex d-md-none justify-center align-center play-btn"
              >
                <v-btn
                  class="d-flex justify-flex-end align-center pr-4"
                  style="background: hsl(242deg 2% 5%)"
                  @click="onGoPlayer(item.contentID, item.contentType)"
                >
                  Play Now
                </v-btn>
              </div>
            </v-col>
          </v-row>
        </v-sheet>
        <!-- </div> -->
      </v-carousel-item>
    </v-carousel>
  </div>
  <div v-else>
    <Preloader />
  </div>
</template>

<script>
  import SliderImg from '../assets/img/slider-1.jpg'
  // import { MenuFeatureItem } from "../types/menuFeatureType";
  import VideoPlayer from '@/components/VodeoPlayer.vue'
  import { devMode } from '../utils/devConfig'
  import Preloader from './Preloader.vue'
  import { getGuestToken, getMovieDetail } from '@/utils/siberapi'

  export default {
    components: {
      Preloader,
      VideoPlayer,
    },
    props: {
      FeaturedSlider: {
        type: Array,
        required: true,
      },
    },
    data() {
      return {
        SliderItems: this.FeaturedSlider,
        SliderImg: SliderImg,
        opacityLevel: devMode ? 0 : 1,
        SVODArray: [],
        movieDetail: [],
      }
    },
    methods: {
      SliderTypeBycontentType(type = '') {
        let sliderType = ''
        switch (type) {
          case 'svod_movies':
            sliderType = 'Film'
            break
          case 'svod_series':
            sliderType = 'Series'
            break
          case 'events':
            sliderType = 'Live Stream Event'
            break
          case 'sports':
            sliderType = 'Sports Event'
            break
        }

        return sliderType
      },
      onGoTailer(contentId = 0, contentType = '') {
        if (contentId) {
          switch (contentType) {
            case 'svod_movies':
              this.$router.push({ path: '/svod/player/' + contentId })
              break
            case 'svod_series':
              this.$router.push({ path: '/svod/player/' + contentId })
              break
            case 'events':
              this.$router.push({ path: '/svod/player/' + contentId })
              break
            case 'sports':
              this.$router.push({ path: '/svod/player/' + contentId })
              break
          }
        }
      },
      setRuntime(val) {
        let hours = 0
        let minutes = 0
        if (val > 60) {
          hours = Math.floor(val / 60)
          minutes = val % 60

          return hours + 'HR ' + minutes + 'M'
        } else {
          return minutes + 'M'
        }
      },
      onGoPlayer(contentId = 0, contentType = '') {
        if (contentId) {
          switch (contentType) {
            case 'svod_movies':
              this.$router.push({ path: '/svod/player/' + contentId })
              break
            case 'svod_series':
              this.$router.push({ path: '/svod/player/' + contentId })
              break
            case 'events':
              this.$router.push({ path: '/svod/player/' + contentId })
              break
            case 'sports':
              this.$router.push({ path: '/svod/player/' + contentId })
              break
          }
        }
      },
      async getMovieDetail(id) {
        let auth = this.$store.getters.getAuth
        let token = auth.auth.msalToken
        let apiParams = {
          token: token,
          vodId: id,
        }
        let response = await getMovieDetail(apiParams)
        return await response.data.response.movie_info
      },
    },
    computed: {},
    watch: {
      FeaturedSlider(newVal) {
        this.SliderItems = newVal
        if (this.SliderItems.length > 0) {
          this.SliderItems.map(async (item) => {
            item.movieDetail = await this.getMovieDetail(item.contentID)
            console.log(item.movieDetail)
            this.movieDetail.push(item)
          })
          this.SliderItems = this.movieDetail
        }
        return newVal
      },
    },
  }
</script>
<style>
  .v-responsive__content {
    padding-left: 8%;
  }
  .v-responsive__content .v-sheet {
    max-width: 38%;
  }

  #film_subject{
    font-size: clamp(1.5rem, 5vw, 3rem) !important;
  }
  
  @media screen and (max-width: 960px) {
    .v-img__img--contain {
      object-fit: cover !important;
    }
    .v-responsive__content {
      padding-left: 0%;
      align-self: end;
      margin-bottom: 50px;
    }
    .v-responsive__content .v-sheet {
      max-width: inherit;
    }
    .film-title {
      margin-top: 40px !important;
    }
    .released-year {
      display: none !important;
    }

    .preview-scene {
      margin-top: 100px !important;
    }
    .carousel_first {
      height: 100vw !important;
    }

    .play-btn {
      margin-top: 10px;
    }

    .play-btn .v-btn__content {
      font-size: 12px;
    }
    .img-title {
      width: 220px !important;
      margin-left: 40px;
    }

    #film_subject {
      padding: 0 10%;
      line-height: 1.2;
    }
    .v-carousel__controls {
      background: #101314 !important;
    }

    .text-subtitle-1,
    .text-h6 {
      line-height: 1.2 !important;
    }
  }

  @media (min-width: 800px) and (max-width: 1100px) {
    .v-responsive__content {
      align-self: center;
    }
  }
</style>
