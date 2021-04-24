<template>
  <div>
    <v-form ref="imageInputForm" class="mt-4">
      <input
        type="file"
        ref="imageInput"
        accept="image/*"
        @change="onImageSeclected"
        hidden
      />
    </v-form>
    <div class="text-h3 text-center mb-5">Phân đoạn hình ảnh</div>
    <v-row>
      <v-col md="8" offset="md-2">
        <v-combobox
          v-model="modelSelected"
          :items="items"
          label="Chọn một mô hình"
          outlined
          filled
        >
        </v-combobox>
      </v-col>
    </v-row>
    <div style="display: flex; justify-content: center;">
      <template v-if="image === ''">
        <v-sheet elevation="1" height="400" width="600" rounded="xl">
          <v-sheet
            elevation="2"
            width="300"
            height="200"
            class="mt-15 mx-auto"
            style="display: flex; border-style: dotted"
            @click="onAddImageClicked"
          >
            <v-icon size="100" style="margin: 0 auto">mdi-plus</v-icon>
          </v-sheet>
          <p class="text-center text-h5 mt-10">Choose Image</p>
        </v-sheet>
      </template>
      <template v-else>
        <v-card width="100%" height="100%">
          <v-img :src="image.data"></v-img>
          <v-divider class="mx-4"></v-divider>
          <v-card-actions>
            <v-btn
              @click="onAddImageClicked($event)"
              icon
              rounded
              color="primary"
              x-large
            >
              <v-icon>mdi-replay</v-icon>
            </v-btn>
            <v-btn @click="onRemoveImageClicked($event)" icon rounded x-large>
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </template>
    </div>
    <v-row justify="center" class="mt-10">
      <v-btn
        color="blue-grey"
        class="ma-2 white--text"
        @click="predictImage"
        width="600"
        height="50"
        rounded
      >
        Predict
        <v-icon right dark>mdi-fast-forward</v-icon>
      </v-btn>
    </v-row>
    <div style="display: flex; justify-content: center;" class="mt-5">
      <template v-if="result !== ''">
      <v-card width="100%" height="100%">
        <v-img :src="getImageDataFromBase64()"></v-img>
        <v-divider class="mx-4"></v-divider>
        <v-card-actions>
          <!-- <v-btn :download="result.name" icon rounded color="primary" x-large>
            <v-icon>mdi-download</v-icon>
          </v-btn> -->
          <a :href="getImageDataFromBase64()" :download="result.name">
            <v-btn :download="result.name" icon rounded color="primary" x-large>
              <v-icon>mdi-download</v-icon>
            </v-btn>
          </a>
          <v-btn @click="onRemoveResultClicked($event)" icon rounded x-large>
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </template>
    </div>
  </div>
</template>
<script>
export default {
  data: () => ({
    dialog: false,
    message: "",
    image: "",
    result: "",
    modelSelected: "",
    items: ["HarDMSEG", "HarDCPD", "PraNet"],
  }),
  methods: {
    onAddImageClicked(event) {
      this.$refs.imageInput.click();
      event.preventDefault();
    },
    onRemoveImageClicked(event) {
      this.image = "";
    },
    onRemoveResultClicked(event) {
      this.result = ''
    },
    onDownloadResult(event) {

    },
    onImageSeclected(event) {
      const reader = new FileReader();
      reader.onload = (e) => {
        this.image = {
          data: e.target.result,
          name: this.$refs.imageInput.files[0].name,
        };
      };
      if (event.target.files[0]) {
        reader.readAsDataURL(this.$refs.imageInput.files[0]);
      }
    },
    async predictImage() {
      this.dialog = true;
      this.result = "";

      if (this.image === "" || this.modelSelected === "") {
        this.dialog = false;
        return;
      }
      let imageBase64 = this.image.data.toString().replace(/^data:(.*,)?/, "");
      if (imageBase64.length % 4 > 0) {
        imageBase64 += "=".repeat(4 - (image.length % 4));
      }
      let modelName = "";
      if (this.modelSelected == "HarDMSEG") {
        modelName = "hardmseg";
      } else if (this.modelSelected == "HarDCPD") {
        modelName = "hardcpd";
      }
      const params = {
        model_name: modelName,
        name: this.image.name,
        base64_encode: imageBase64,
      };
      console.log(params);
      try {
        const resp = await this.$axios.$post(
          `${process.env.apiBaseUrl}/predict`,
          params
        );
        console.log(resp);
        if (resp.message === "Success") {
          this.result = {}
          this.result.base64 = resp.base64_encode;
          this.result.name = resp.name
        }
        console.log(this.result);

        setTimeout(() => {}, 500);
        this.dialog = false;
      } catch (error) {}
    },
    getImageDataFromBase64() {
      return `data:image/jpeg;base64,${this.result.base64}`;
    },
  },
};
</script>