# Vuetify3 Starter

## initilize nuxt3 application
1. npm nuxi init nuxt3app
    ```
    ➜  workspace git:(master) ✗ npx nuxi init nuxt3app
    Nuxi 3.5.2                                                                                                                                                     8:19:57 AM
    ✨ Nuxt project is created with v3 template. Next steps:                                                                                                       8:19:57 AM
    › cd nuxt3app                                                                                                                                                 8:19:57 AM
    › Install dependencies with npm install or yarn install or pnpm install                                                                                       8:19:57 AM
    › Start development server with npm run dev or yarn dev or pnpm run dev                    
    ```

2. npm install
    ```
    ➜  workspace git:(master) ✗ cd nuxt3app 
    ➜  nuxt3app git:(master) ✗ npm install

    > postinstall
    > nuxt prepare

    Nuxi 3.5.2                                                                                                                                                     8:22:44 AM
    ✔ Types generated in .nuxt                                                                                                                                     8:22:46 AM

    added 614 packages, and audited 615 packages in 34s

    95 packages are looking for funding
    run `npm fund` for details

    found 0 vulnerabilities
    ```

3. npm run dev
    ```
    Nuxi 3.5.2                                                                                                                                                     8:24:41 AM
    Nuxt 3.5.2 with Nitro 2.4.1                                                                                                                                    8:24:41 AM
                                                                                                                                                                8:24:42 AM
    > Local:    http://localhost:3000/ 
    > Network:  http://192.168.241.2:3000/

    ℹ Vite client warmed up in 1248ms                                                                                                                              8:24:44 AM
    ✔ Nitro built in 795 ms          
    ```
    
## install Vuetify3
1. npm install vuetify
    ```
    ➜  nuxt3app git:(master) ✗ npm install vuetify

    added 1 package, and audited 616 packages in 4s

    96 packages are looking for funding
    run `npm fund` for details

    found 0 vulnerabilities
    ```

2. Material Design iconのインストール
    ```
    ➜  nuxt3app git:(master) ✗ npm install @mdi/font

    added 1 package, and audited 617 packages in 1s

    96 packages are looking for funding
    run `npm fund` for details

    found 0 vulnerabilities
    ```

3. バージョンの確認
* package.json
    ```
    "dependencies": {
        "@mdi/font": "^7.2.96",
        "vuetify": "^3.3.2"
    }
    ```

## setup Vuetify3
1. nuxt.config.tsの編集
    * SSR: server side renderingをfalse
    * materialdesigniconsへのCSSを指定
    ```
    export default defineNuxtConfig({
        ssr: false,
        css: ["vuetify/styles", "@mdi/font/css/materialdesignicons.css"],
    });    
    ```
    
2. pluginの作成
    1. pluginsディレクトリを作成
    2. plugins/vuetify.tsを作成
        ```
        import { createVuetify } from "vuetify";
        import * as components from "vuetify/components";
        import * as directives from "vuetify/directives";

        export default defineNuxtPlugin((nuxtApp) => {
        const vuetify = createVuetify({
            components,
            directives,
        });

        nuxtApp.vueApp.use(vuetify);
        });       
        ```    
        
## implement vuetify samples
* Vuetify3/Componentから任意のサンプルコード(template/script)を抽出し、app.vueを置き換える。
    * [Buttons](https://vuetifyjs.com/en/components/buttons/)
    * [Tables](https://vuetifyjs.com/en/components/tables/)

* app.vue
    * Vuetify3のサンプルコードのOption API部分はComposition APIに置き換えている。
    
    ```
<template>
  <v-container>
    <v-row align="center" justify="center">
      <v-col cols="auto">
        <v-btn density="compact" icon="mdi-plus"></v-btn>
      </v-col>

      <v-col cols="auto">
        <v-btn density="comfortable" icon="$vuetify"></v-btn>
      </v-col>

      <v-col cols="auto">
        <v-btn density="default" icon="mdi-open-in-new"></v-btn>
      </v-col>
    </v-row>

    <v-row align="center" justify="center">
      <v-col cols="auto">
        <v-btn icon="mdi-account" size="x-small"></v-btn>
      </v-col>

      <v-col cols="auto">
        <v-btn icon="mdi-plus" size="small"></v-btn>
      </v-col>

      <v-col cols="auto">
        <v-btn icon="$vuetify"></v-btn>
      </v-col>

      <v-col cols="auto">
        <v-btn icon="mdi-open-in-new" size="large"></v-btn>
      </v-col>

      <v-col cols="auto">
        <v-btn icon="mdi-calendar" size="x-large"></v-btn>
      </v-col>
    </v-row>
  </v-container>
  <v-table fixed-header height="300px">
    <thead>
      <tr>
        <th class="text-left">Name</th>
        <th class="text-left">Calories</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="item in desserts" :key="item.name">
        <td>{{ item.name }}</td>
        <td>{{ item.calories }}</td>
      </tr>
    </tbody>
  </v-table>
</template>
<script setup>
import { ref } from "vue";
const desserts = ref([
  {
    name: "Frozen Yogurt",
    calories: 159,
  },
  {
    name: "Ice cream sandwich",
    calories: 237,
  },
  {
    name: "Eclair",
    calories: 262,
  },
  {
    name: "Cupcake",
    calories: 305,
  },
  {
    name: "Gingerbread",
    calories: 356,
  },
  {
    name: "Jelly bean",
    calories: 375,
  },
  {
    name: "Lollipop",
    calories: 392,
  },
  {
    name: "Honeycomb",
    calories: 408,
  },
  {
    name: "Donut",
    calories: 452,
  },
  {
    name: "KitKat",
    calories: 518,
  },
]);
</script>
    ```

* アプリケーション画面

    ![](./vuetify1.png)
