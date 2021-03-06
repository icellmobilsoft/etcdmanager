<template>
    <v-navigation-drawer v-model="drawer" clipped fixed app>
        <v-list dense>
            <v-list-tile ripple to="/configure">
                <v-list-tile-action>
                    <v-icon data-test="menu.configure.icon">settings</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title
                        data-test="menu.configure.list-tile-title"
                    >{{ $t('menu.settings') }}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
            <v-list-tile ripple to="/cluster" :disabled="!isLimited">
                <v-list-tile-action>
                    <v-icon data-test="menu.cluster.icon">cloud_circle</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title
                        data-test="menu.cluster.list-tile-title"
                    >{{ $t('menu.manageCluster') }}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
            <v-list-tile ripple to="/keys">
                <v-list-tile-action>
                    <v-icon data-test="menu.keys.icon">list</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title
                        data-test="menu.keys.list-tile-title"
                    >{{ $t('menu.manageKeys') }}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
            <v-list-tile ripple to="/watchers">
                <v-list-tile-action>
                    <v-icon data-test="menu.watchers.icon">remove_red_eye</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title
                        data-test="menu.watchers.list-tile-title"
                    >{{ $t('menu.manageWatchers') }}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
            <v-list-tile ripple to="/users" :disabled="!isLimited">
                <v-list-tile-action>
                    <v-icon data-test="menu.users.icon">person</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title
                        data-test="menu.users.list-tile-title"
                    >{{ $t('menu.manageUsers') }}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
               <v-list-tile ripple to="/leases" :disabled="!isLimited || isOlder(3.3)">
                <v-list-tile-action>
                    <v-icon data-test="menu.leases.icon">av_timer</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title
                        data-test="menu.users.list-tile-title"
                    >{{ $t('menu.manageLeases') }}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
            <v-list-tile ripple to="/roles" :disabled="!isLimited">
                <v-list-tile-action>
                    <v-icon data-test="menu.roles.icon">verified_user</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title
                        data-test="menu.roles.list-tile-title"
                    >{{ $t('menu.manageRoles') }}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
            <v-list-tile ripple to="/about">
                <v-list-tile-action>
                    <v-icon data-test="menu.about.icon">info</v-icon>
                </v-list-tile-action>
                <v-list-tile-content>
                    <v-list-tile-title data-test="menu.about.list-tile-title">{{ $t('menu.about') }}</v-list-tile-title>
                </v-list-tile-content>
            </v-list-tile>
        </v-list>
    </v-navigation-drawer>
</template>

<script lang="ts">
import Vue from 'vue';
import { Component } from 'vue-property-decorator';
import { AuthService } from '../services/auth.service';

@Component({
    name: 'main-menu',
    props: {
        source: String,
        drawer: Boolean,
    },
})
export default class Menu extends Vue {

    public authService: AuthService;

    constructor() {
        super();
        this.authService = new AuthService();
    }

    get isLimited() {
        return this.$store.state.isLimited;
    }

    isOlder(version: number) {
        return this.$store.state.etcd.version < version;
    }

    public isActive(menuItem: string) {
        return this.$route.name === menuItem;
    }
}
</script>

<style scoped>
</style>
