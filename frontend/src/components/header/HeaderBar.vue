<template>
  <header>
    <a href="/">
      <img v-if="showLogo !== undefined" :src="logoURL" alt="logo" />
    </a>
    <action
      v-if="showMenu !== undefined"
      class="menu-button"
      icon="menu"
      :label="$t('buttons.toggleSidebar')"
      @action="openSidebar()"
    />

    <slot />

    <div id="dropdown" :class="{ active: this.$store.state.show === 'more' }">
      <slot name="actions" />
    </div>

    <action
      v-if="this.$slots.actions"
      id="more"
      icon="more_vert"
      :label="$t('buttons.more')"
      @action="$store.commit('showHover', 'more')"
    />

    <div
      class="overlay"
      v-show="this.$store.state.show == 'more'"
      @click="$store.commit('closeHovers')"
    />
  </header>
</template>

<script>
import { logoURL } from "@/utils/constants";

import Action from "@/components/header/Action";

export default {
  name: "header-bar",
  props: ["showLogo", "showMenu"],
  components: {
    Action,
  },
  data: function () {
    return {
      logoURL,
    };
  },
  methods: {
    openSidebar() {
      this.$store.commit("showHover", "sidebar");
    },
  },
};
</script>

<style></style>
