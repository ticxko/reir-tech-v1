<script setup lang="ts">
import { ref, shallowRef } from 'vue';
import { useCustomizerStore } from '@/stores/customizer';
import sidebarItems from './sidebarItem';

import NavGroup from './NavGroup/index.vue';
import NavItem from './NavItem/index.vue';
import NavCollapse from './NavCollapse/NavCollapse.vue';
import ExtraBox from './extrabox/ExtraBox.vue';
import Moreoption from './MoreOption/Moreoption.vue';
import Logo from '../logo/Logo.vue';
import { useAuthStore } from '@/stores/auth';
import { Icon } from '@iconify/vue';


const customizer = useCustomizerStore();
const sidebarMenu = shallowRef(sidebarItems);
const authStore = useAuthStore();
</script>

<template>
   
        <v-navigation-drawer left v-model="customizer.Sidebar_drawer" rail-width="70" app
            class="leftSidebar ms-lg-5 mt-sm-5 bg-containerBg" elevation="10" :rail="customizer.mini_sidebar"
            expand-on-hover width="270">
            <div class="pa-5 pl-4 ">
                <Logo />
            </div>
            <!-- ---------------------------------------------- -->
            <!---Navigation -->
            <!-- ---------------------------------------------- -->
            <perfect-scrollbar class="scrollnavbar bg-containerBg overflow-y-hidden">

                <v-list class="py-4 px-4 bg-containerBg">
                    <!---Menu Loop -->
                    <template v-for="(item, i) in sidebarMenu">
                        <!---Item Sub Header -->
                        <NavGroup :item="item" v-if="item.header" :key="item.title" />
                        <!---If Has Child -->
                        <NavCollapse class="leftPadding" :item="item" :level="0" v-else-if="item.children" />
                        <!---Single Item-->
                        <NavItem :item="item" v-else class="leftPadding" />
                        <!---End Single Item-->
                    </template>
                    <!-- <Moreoption/> -->
                </v-list>
                <div class="pa-6 px-4 userbottom bg-containerBg mt-10">
                    <ExtraBox />
                </div>
            </perfect-scrollbar>
        </v-navigation-drawer>
        
</template>
