<template>
  <div class="mt-10">
    <v-row>
      <v-col cols="3">
        <v-img src="/pranet.png" height="200" width="200"></v-img>
      </v-col>
      <v-col cols="9">
        <div class="text-h3">Một số mô hình tiêu biểu</div>
        <v-row class="mt-5">
          <v-col cols="3">
            <span class="font-weight-black">{{ models.length }}</span>
            <span>Mô hình</span>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
    <v-divider class="mt-10"></v-divider>
    <div class="mt-10">
      <div class="text-h4">Mô tả</div>
    </div>
    <v-divider class="mt-10"></v-divider>
    <div class="mt-10">
      <div class="text-h4">Các mô hình</div>
      <v-row class="mt-5">
        <v-col v-for="(index, model) in models" :key="model.title" sm="4">
          <v-card rounded="xl" height="650" elevation="3">
            <v-card-title>
              {{ model.title }}
              <v-spacer></v-spacer>
              <v-btn icon :to="model.to">
                <v-icon>mdi-arrow-right-bold</v-icon>
              </v-btn>
            </v-card-title>
            <v-divider class="mx-4"></v-divider>
            <v-img :src="model.image" class="mt-5"></v-img>
          </v-card>
        </v-col>
        <div class="text-center">
          <v-pagination v-model="page" :length="models.length / 2" circle></v-pagination>
        </div>
      </v-row>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({
    models: [
      {
        title: "HardMSEG",
        image: "/hardmseg.png",
        description: "",
        to: "/models/hardmseg",
        link: "",
      },
      {
        title: "PraNet",
        image: "/pranet.png",
        description: "",
        to: "/models/hardmseg",
        link: "",
      },
      {
        title: "FANet",
        image: "/fanet.png",
        description: "",
        to: "/models/hardmseg",
        link: "https://arxiv.org/pdf/2103.17235v1.pdf",
      },
      {
        title: "ResUNet++",
        image: "/resunet++.png",
        description: "",
        to: "/models/hardmseg",
        link: "https://arxiv.org/pdf/1911.07067v1.pdf",
      },
      {
        title: "TransFuse Net",
        image: "/transfusenet.png",
        description: "",
        to: "/models/hardmseg",
        link: "",
      },
      {
        title: "UNet-ResNet50",
        image: "unet.png",
        description: "",
        to: "/models/hardmseg",
        link: "",
      },
    ],
    page: 1
  }),
  methods: {},
};
</script>