<template>
  <div class="vf-home">
    <b-row>
      <b-col md="9">
        <re-build v-show="!cms.generating" />
        <welcome
          v-if="cms.builds.length === 0"
          v-show="!cms.generating"
        />
        <activity v-if="cms.builds.length > 0 || cms.generating" />
        <first-build v-if="firstBuild" />
        <development />
      </b-col>
      <b-col md="3">
        <subscription v-if="false" />
        <information />
      </b-col>
    </b-row>
  </div>
</template>
<script>
import {mapGetters} from 'vuex'
import Subscription from '~/components/subscription'
import Development from '~/components/development'
import Information from '~/components/information'
import Activity from '~/components/activity'
import Welcome from '~/components/welcome'
import ReBuild from '~/components/rebuild'
import FirstBuild from '~/components/firstBuild'
export default {
  components: {
    Subscription,
    Information,
    Development,
    Activity,
    Welcome,
    ReBuild,
    FirstBuild
  },
  async fetch(ctx) {
    await ctx.store.dispatch('information/load')
  },
  middleware: ['authenticated', 'confirmed', 'noBanned', 'noAlien'],
  computed: {
    ...mapGetters({information: 'information/get', cms: 'cms/get', firstBuild: 'cms/firstBuild'})
  }
}
</script>
<style lang="scss">
.vf-home {

  &__rebuild {
    margin-bottom: 30px !important;
    padding: 20px !important;
    &_description {
      font-size: 1.3rem;
    }
  }
}
</style>
