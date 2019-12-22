<template>
  <div class="row row-equal">
    <div class="flex xs12">
      <p class="display-2">Devices</p>
    </div>
    <div class="flex xs12">
      <div v-if="!devices" class="row">
        <va-progress-bar 
          class="placeholder small"
          color="success"
          :indeterminate="true"
        />
      </div>
      <div v-if="devices" class="row">

        <div
          class="flex xs12 sm6 md4 xl2"
          v-for="(device, id) in devices"
          @click="changeDevice(device.ID)"
          :key="id"
        >
          <va-card class="mb-4 card-device" :color="device.ID == selected ? 'info' : 'gray'">
            <p class="display-2 mb-0" style="color: white">{{ device.DeviceName }}</p>
            <p>{{device.StationName}}</p>
          </va-card>
        </div>
      </div>
      <!--
      <div class="row">
        <div class="flex xs12 md6">
          <va-card>
            <p class="display-2 mb-1" :style="{color: this.$themes.primary}">291</p>
            <p class="no-wrap">{{$t('dashboard.info.completedPullRequests')}}</p>
          </va-card>
        </div>
        <div class="flex xs12 md6">
          <va-card>
            <div class="row row-separated">
              <div class="flex xs4">
                <p class="display-2 mb-1 text--center" :style="{color: this.$themes.primary}">3</p>
                <p class="text--center mb-1">{{$t('dashboard.info.users')}}</p>
              </div>
              <div class="flex xs4">
                <p class="display-2 mb-1 text--center" :style="{color: this.$themes.info}">24</p>
                <p class="text--center no-wrap mb-1">{{$t('dashboard.info.points')}}</p>
              </div>
              <div class="flex xs4">
                <p class="display-2 mb-1 text--center" :style="{color: this.$themes.warning}">91</p>
                <p class="text--center mb-1">{{$t('dashboard.info.units')}}</p>
              </div>
            </div>
          </va-card>
        </div>
      </div>
      -->
    </div>

    <!--
    <div class="flex xs12 md6 xl3">
      <va-card
        stripe="info"
        :title="$t('dashboard.info.componentRichTheme')"
      >
        Buying the right telescope to take your love of astronomy to the
        next level is a big next step.

        <div class="row mt-3">
          <va-button color="success">
            {{$t('dashboard.info.viewLibrary')}}
          </va-button>
        </div>
      </va-card>
    </div>
    <div class="flex xs12 md6 xl3">
      <va-card
        image="https://i.imgur.com/qSykGko.jpg"
        square
        titleOnImage
      >
        <template slot="header">
          <va-button
            flat
            icon-right="ion ion-ios-arrow-forward"
            color="success"
            class="ma-0"
          >
            {{$t('dashboard.info.exploreGallery')}}
          </va-button>
        </template>
      </va-card>
    </div>
    -->
  </div>
</template>

<script>
export default {
  name: 'devices-info-block',
  props: ['devices', 'selected', 'changeDevice'],
  data () {
    return {
      
    }
  },
}
</script>

<style lang="scss">
  .row-separated {
    .flex + .flex {
      border-left: 1px solid #e3eaeb;
    }

    @include media-breakpoint-down(xs) {
      p:not(.display-2){
        font-size: 0.875rem;
      }
    }
  }

  .dashboard {
    .va-card__header--over {
      @include media-breakpoint-up(md) {
        padding-top: 0 !important;
      }
    }

    .va-card__image {
      @include media-breakpoint-up(md) {
        padding-bottom: 0 !important;
      }
    }
  }
</style>
