<template>
  <v-flex>
    <v-card class="mx-3 py-0 mt-2" outlined tile>
      <v-card-title class="py-2"> แบรนด์ </v-card-title>
    </v-card>
    <v-flex>
      <v-container>
        <v-row>
          <v-col sm="1" v-for="item in ProductBrands" :key="item.ID">
            <BrandCard :BrandData="item" />
          </v-col>
        </v-row>
      </v-container>
    </v-flex>
    <v-card class="mx-3" outlined tile>
      <v-card-title class="py-2"> ประเภท </v-card-title>
    </v-card>
    <v-flex>
      <v-container>
        <v-row>
          <v-col sm="1" v-for="item in ProductType" :key="item.ID">
            <CatagoryCard :TypeData="item" />
          </v-col>
        </v-row>
      </v-container>
    </v-flex>
    <v-card> </v-card>
    <v-card class="mx-3" outlined tile>
      <v-card-title class="py-2">สินค้าแนะนำ </v-card-title>
    </v-card>
    <v-flex>
      <v-container>
        <v-row>
          <v-col sm="3" v-for="item in Products" :key="item.ID">
            <v-flex v-if="item.ProdQty > 0 && item.ProdImage !== null">
              <ProductsProductCard :ProductData="item" />
            </v-flex>
          </v-col>
        </v-row>
      </v-container>
    </v-flex>
  </v-flex>
</template>

<script>
export default {
  name: "IndexPage",
  data: () => {
    return {
      Products: [],
      ProductBrands: [],
      ProductType: [],
    };
  },
  methods: {
    async GetProduct() {
      const res = await this.$axios.$get("/Products");
      this.Products = res;
      this.Products = this.Products.filter((p) => p.ProdQty > 0);
    },
    async GetBrand() {
      const res = await this.$axios.$get("/Brand");
      this.ProductBrands = res;

      // this.ProductBrands.map(p => p.q)
    },
    async GetType() {
      const res = await this.$axios.$get("/Type");
      console.log(res);
      this.ProductType = res;
    },
  },
  mounted() {
    this.GetProduct();
    this.GetBrand();
    this.GetType();
  },
};
</script>
