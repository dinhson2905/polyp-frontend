<template>
  <div>
    <v-row class="mt-10">
      <v-col cols="3">
        <v-img src="/medical-overview.png" height="200" width="200"></v-img>
      </v-col>
      <v-col cols="9">
        <div class="text-h3">Phân đoạn Polyb trong đường tiêu hóa</div>
        <v-row class="mt-5">
          <v-col cols="3">
            <span class="font-weight-black">{{ models.length }}</span>
            <span>Mô hình</span>
          </v-col>
          <v-col cols="3">
            <span class="font-weight-black">{{ datasets.length }}</span>
            <span>Bộ dữ liệu</span>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
    <v-divider class="mt-10"></v-divider>
    <div class="mt-10">
      <div class="text-h4">Giới thiệu</div>
      <p class="mt-5">
        <b>Ung thư đại trực tràng</b> là nguyên nhân gây tử vong rất cao. Có thể
        chẩn đoán sớm ung thư đại trực tràng nếu polyp đại trực tràng (tiền thân
        của ung thư) được phát hiện và cắt bỏ trước khi phát triển thành ác
        tính.
      </p>
      <p>
        <b>Polyp</b> là phần nhô ra khỏi bề mặt đại tràng. Polyp xuất hiện với
        nhiều hình dạng khác nhau, từ dạng phẳng đến dạng cục. Nội soi đại tràng
        là một thủ thuật phụ thuộc vào người thực hiện, trong đó các yếu tố con
        người như mệt mỏi và không chú ý đầy đủ có thể dẫn đến việc bỏ sót các
        polyp trong quá trình kéo dài.
      </p>
      <p>
        <b>Sự hỗ trợ của máy tính</b> có thể giúp các bác sĩ nội soi thực hiện
        nhiệm vụ phát hiện polyp và có thể khuyến khích sự chú ý hơn trong quá
        trình làm thủ thuật.
      </p>
      <p>
        <b>Hệ thống phát hiện polyp</b> đáng tin cậy phải xử lý sự thay đổi của
        polyp về hình dạng, kích thước, màu sắc và kết cấu. Một hệ thống như vậy
        có thể cứu được nhiều mạng sống!
      </p>
      <p>
        <b>Phân đoạn Polyb trong đường tiêu hóa</b> là nhiệm vụ phân đoạn các
        polyb trong một hình ảnh y tế.
      </p>
      <p></p>
      <p>
        <b>Deep learning</b> đã được sử dụng rộng rãi trong phân đoạn polyb
        trong đường tiêu hóa và có một số paper ghi lại thành công trong lĩnh
        vực này.
      </p>
    </div>
    <v-divider class="mt-10"></v-divider>
    <div class="text-h4 mt-10">Các nhiệm vụ liên quan</div>
    <p class="mt-5">
      <b>Học giám sát (Supervised learning)</b> là phương pháp phổ biến nhất để
      phân đoạn polyb trong đường tiêu hóa. Để cải tiến một kiến trúc mạng
      nơ-ron (neural network) ta có thể xem xét các khía cạnh sau:
    </p>
    <v-expansion-panels>
      <v-expansion-panel>
        <v-expansion-panel-header
          ><b
            >Lựa chọn mạng xương sống (Backbone Networks)</b
          ></v-expansion-panel-header
        >
        <v-expansion-panel-content>
          <p>
            Phân đoạn ngữ nghĩa hình ảnh nhằm đạt được sự phân loại pixel của
            một hình ảnh. Với mục đích này, cấu trúc encoder-decoder đã được đưa
            ra. Encoder thường trích trọn đặc trưng của hình ảnh Trong khi đó,
            Decoder khôi phục các đặc trưng đã trích xuất về kích thước ảnh ban
            đầu và xuất ra kết quả phân đoạn cuối cùng.
          </p>
          <p>UNet, RNN, Skip Connection, Casecade 2D, ...</p>
        </v-expansion-panel-content>
      </v-expansion-panel>
      <v-expansion-panel>
        <v-expansion-panel-header>
          <b>Thiết kế khối mạng (Network Function Blocks)</b>
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          <ul>
            <li>
              <b>Dense Connection:</b> đầu vào của mỗi lớp đến từ đầu ra của tất
              cả các lớp trước đó trong quá trình chuyển tiếp truyền tải.
            </li>
            <li>
              <b>Inception:</b> Cấu trúc này có thể trích xuất các tính năng
              hình ảnh phong phú hơn bằng cách sử dụng nhân chập nhiều tỷ lệ và
              thực hiện hợp nhất đối tượng để có được biểu diễn đối tượng tốt
              hơn.
            </li>
            <li>
              <b>Cơ chế Attention:</b> Attention block có thể thay đổi đầu vào một cách
              chọn lọc hoặc gán các trọng số khác nhau cho các biến đầu vào theo
              mức độ quan trọng khác nhau.
            </li>
            <li>...</li>
          </ul>
        </v-expansion-panel-content>
      </v-expansion-panel>
      <v-expansion-panel>
        <v-expansion-panel-header>
          <b>Cải tiến hàm mất mát (Loss functions)</b>
        </v-expansion-panel-header>
        <v-expansion-panel-content>
          <p>
            Việc lựa chọn và kết hợp các hàm mất mát cũng là một yếu tố quan
            trọng để cải thiện hiệu suất mạng.
          </p>
          <ul>
            <li>Cross Entropy Loss</li>
            <li>Weighted Cross Entropy Loss</li>
            <li>Dice Loss</li>
            <li>IoU Loss</li>
            <li>Generalized Dice Loss</li>
            <li>Boundary Loss</li>
            <li>...</li>
          </ul>
        </v-expansion-panel-content>
      </v-expansion-panel>
    </v-expansion-panels>
    <v-divider class="mt-10"></v-divider>
    <div>
      <div class="mt-10 text-h4">Các bộ dữ liệu</div>
      <v-row class="mt-5">
        <v-col v-for="dataset in datasets" :key="dataset.title" sm="3">
          <v-card width="300" rounded="xl" height="500">
            <v-card-title>
              {{ dataset.title }}
            </v-card-title>
            <v-img :src="dataset.image" height="200" width="300"></v-img>
            <v-divider class="mx-4"></v-divider>
            <v-card-text>{{ dataset.description }}</v-card-text>
            <v-card-actions>
              <v-btn color="blue-grey lighten-1" text> Xem thêm </v-btn>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>
    </div>
    <v-sheet height="100"></v-sheet>
  </div>
</template>

<script>
export default {
  data: () => ({
    models: [{ title: "HardMSEG" }, { title: "PraNet" }, { title: "ResNet" }],
    datasets: [
      {
        title: "Kvasir-SEG",
        image: "/Kvasir.png",
        description:
          "Kvasir-SEG gồm 1000 hình ảnh polyp đường tiêu hóa và mặt nạ phân đoạn tương ứng, được chú thích và xác thực bởi bác sĩ chuyên khoa tiêu hóa có kinh nghiệm.",
      },
      {
        title: "CVC-ClinicDB",
        image: "/CVC-ClinicDB.png",
        description:
          "CVC-ClinicDB gồm 612 hình ảnh với độ phân giải 384×288 từ 31 chuỗi nội soi đại tràng, được sử dụng để phân đoạn, phát hiện polyp trong video nội soi đại tràng.",
      },
      {
        title: "CVC-ConlonDB",
        image: "/CVC-ColonDB.png",
        description:
          "CVC-ColonDB gồm các chuỗi video có chú thích của video nội soi đại tràng. Nó chứa 15 chuỗi nội soi đại tràng ngắn, đến từ 15 nghiên cứu khác nhau. Trong mỗi trình tự, một polyp được hiển thị.",
      },
      {
        title: "ETIS-Larib",
        image: "/ETIS.png",
        description:
          "ETIS-Larib Polyp DB gồm các khung được trích xuất từ ​​các video nội soi đại tràng, cung cấp ví dụ về polyp và mặt nạ tương ứng.",
      },
    ],
    subtasks: [
      { title: "", image: "" },
      { title: "", image: "" },
      { title: "", image: "" },
      { title: "", image: "" },
      { title: "", image: "" },
    ],
  }),
};
</script>
