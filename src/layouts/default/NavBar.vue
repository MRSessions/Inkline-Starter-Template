<template>
   <i-navbar collapse="xs" class="_position:sticky-top" fluid>
      <i-navbar-brand to="/">Inkline Starter Template</i-navbar-brand>
      <i-navbar-collapsible class="_justify-content:flex-end">
         <i-nav>
            <i-nav class="_padding-right:3">
               <i-nav-item to="/">
                  Home
               </i-nav-item>
               <i-nav-item to="/about">
                  About
               </i-nav-item>
            </i-nav>
            <IconSun class="_sm:visible" v-if="colorMode === 'dark'" @click="setColorMode"/>
            <IconMoon class="_sm:visible" v-else @click="setColorMode"/>
            <i-nav-item class="_text-align:center _sm:hidden">
               <div v-if="colorMode === 'dark'" @click="setColorMode"><IconSun></IconSun> Light</div>
               <div v-else @click="setColorMode"><IconMoon></IconMoon> Dark</div>
            </i-nav-item>
         </i-nav>
      </i-navbar-collapsible>
   </i-navbar>
</template>

<script setup>
import { inject, ref } from 'vue';
import IconSun from './icons/IconSun.vue';
import IconMoon from './icons/IconMoon.vue';

const inkline = inject('inkline');
const colorMode = ref(inkline.options.colorMode)

if (colorMode.value === 'system' && typeof window !== 'undefined') {
   colorMode.value = window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light';
}

const setColorMode = () => {
   const mode = colorMode.value === 'dark' ? 'light' : 'dark';

   inkline.options.colorMode = mode;
   colorMode.value = mode;
}
</script>