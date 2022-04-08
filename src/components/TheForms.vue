<script>
import Slider from "@vueform/slider";
import slotCard from "@/components/slot/slotCard.vue";
import slotCardHeader from "@/components/slot/slotCardHeader.vue";

export default {
  components: {
    Slider,
    slotCard,
    slotCardHeader
  },
  data() {
    return {
      productName: "",
      sellers: [
        {
          status: true,
          name: "فروشنده رسمی",
          enName: "officialSeller"
        },
        {
          status: false,
          name: "فروشنده برگزیده",
          enName: "selectedSeller"
        },
        {
          status: true,
          name: "دیجی کالا",
          enName: "digiKalaSeller"
        },
        {
          status: false,
          name: "کسب و کارهای بومی",
          enName: "indigenousBusinessesSeller"
        }
      ],
      sellerType: [],
      productStatus: false,
      sellerTypeActiveSelected: "All",
      category: [
        {
          status: false,
          name: "کالای دیجیتال",
          enName: "Digital",
          brands: [
            {
              name: "برند یک دیجیتال",
              enName: "brand1Digital"
            },
            {
              name: "برند دوم دیجیتال",
              enName: "brand2Digital"
            },
            {
              name: "برند سوم دیجیتال",
              enName: "brand3Digital"
            },
            {
              name: "برند چهارم دیجیتال",
              enName: "brand4Digital"
            }
          ],
          priceRang: [0, 100]
        },
        {
          status: false,
          name: "کتاب لوازم والتحریر",
          enName: "Book",
          brands: [
            {
              name: "برند یک کتاب",
              enName: "brand1Book"
            },
            {
              name: "برند دوم کتاب",
              enName: "brand2Book"
            },
            {
              name: "برند سوم کتاب",
              enName: "brand3Book"
            },
            {
              name: "برند چهارم کتاب",
              enName: "brand4Book"
            }
          ],
          priceRang: [0, 100]
        },
        {
          status: false,
          name: "خانه و آشپزخانه",
          enName: "Home",
          brands: [
            {
              name: "برند یک خانه",
              enName: "brand1Home"
            },
            {
              name: "برند دوم خانه",
              enName: "brand2Home"
            }
          ],
          priceRang: [0, 100]
        },
        {
          status: false,
          name: "سلامت و زیبایی",
          enName: "Health",
          brands: [
            {
              name: "برند یک سلامت",
              enName: "brand1Health"
            },
            {
              name: "برند دوم سلامت",
              enName: "brand2Health"
            },
            {
              name: "برند سوم سلامت",
              enName: "brand3Health"
            }
          ],
          priceRang: [0, 100]
        }
      ],
      categorySelected: "",
      brandSelected: [],
      categoryDetail: false,
      fullQuery: "http://localhost:3000/q?"
    };
  },
  computed: {
    sellerTypeActive() {
      return this.sellers.filter(item => item.status === true);
    },
    categoryActive() {
      return this.category.filter(item => item.status === true);
    },
    myQuery() {
      let rangeValue = undefined;
      this.categoryActive.forEach((element) => {
        rangeValue = element.priceRang.toString().replaceAll(",", "--");
      });

      // const paramsProductName = this.productName.length > 0 ? "productName~" + this.productName : undefined;
      // const paramsSellerType = this.sellerType.length > 0 ? "sellerType~" + this.sellerType.toString().replaceAll(",", "--") : undefined;
      // const paramsProductStatus = this.productStatus === true ? "productStatus~" + this.productStatus : undefined;
      // const paramsSellerTypeActiveSelected = this.sellerTypeActiveSelected.length > 0 && this.sellerTypeActiveSelected !== "All" ? "sellerTypeActiveSelected~" + this.sellerTypeActiveSelected : undefined;
      // const paramsCategorySelected = this.categorySelected.length > 0 ? "categorySelected~" + this.categorySelected : undefined;
      // const paramsBrandSelected = this.brandSelected.length > 0 && this.categorySelected.length > 0 ? "brandSelected~" + this.brandSelected.toString().replaceAll(",", "--") : undefined;
      // const paramsPriceRang = this.categorySelected.length > 0 ? "priceRang~" + rangeValue : undefined;

      const paramsProductName = this.productName.length > 0 ? this.productName : undefined;
      const paramsSellerType = this.sellerType.length > 0 ? this.sellerType.toString().replaceAll(",", "--") : undefined;
      const paramsProductStatus = this.productStatus === true ? this.productStatus : undefined;
      const paramsSellerTypeActiveSelected = this.sellerTypeActiveSelected.length > 0 && this.sellerTypeActiveSelected !== "All" ? this.sellerTypeActiveSelected : undefined;
      const paramsCategorySelected = this.categorySelected.length > 0 ? this.categorySelected : undefined;
      const paramsBrandSelected = this.brandSelected.length > 0 && this.categorySelected.length > 0 ? this.brandSelected.toString().replaceAll(",", "--") : undefined;
      const paramsPriceRang = this.categorySelected.length > 0 ? rangeValue : undefined;


      this.$router.replace({
        query: {
          productName: paramsProductName,
          sellerType: paramsSellerType,
          productStatus: paramsProductStatus,
          sellerTypeActiveSelected: paramsSellerTypeActiveSelected,
          categorySelected: paramsCategorySelected,
          brandSelected: paramsBrandSelected,
          priceRang: paramsPriceRang
        }
      });

      // window.location.href = history.state.current.replaceAll("&", "+").replaceAll("=", "~");

      return this.$route.query;
    }
  },
  methods: {
    showBrand(index) {
      this.categoryDetail = true;
      this.category.forEach(item => item.status = false);
      this.category[index].status = true;
    },
    clearBrands() {
      this.sellers.filter(item => item.status === false);
      this.sellerTypeActiveSelected = "All";
    },
    clearCategory() {
      this.brandSelected = [];
      this.category.filter(item => item.priceRang = [0, 100]);
    },
    clearFilter(filterName) {
      switch (filterName) {
        case "productName":
          this.productName = "";
          break;
        case "sellerType":
          this.sellerType = [];
          break;
        case "productStatus":
          this.productStatus = false;
          this.sellerTypeActiveSelected = "All";
          break;
        case "categorySelected":
          this.categorySelected = "";
          this.categoryDetail = false;
          break;
        case "brandSelected":
          this.brandSelected = [];
          break;
        case "priceRang":
          this.category.filter(item => item.priceRang = [0, 100]);
          break;
      }
    },
    clearAllFilter() {
      this.clearFilter("productName");
      this.clearFilter("sellerType");
      this.clearFilter("productStatus");
      this.clearFilter("categorySelected");
      this.clearFilter("brandSelected");
      this.clearFilter("priceRang");
    }
  },
  mounted() {
    if (this.$route.query.productName !== undefined) {
      this.productName = this.$route.query.productName;
    }
    if (this.$route.query.sellerType !== undefined) {
      this.sellerType = this.$route.query.sellerType.split("--");
    }
    if (this.$route.query.productStatus !== undefined) {
      this.productStatus = true;
    }
    if (this.$route.query.sellerTypeActiveSelected !== undefined) {
      this.sellerTypeActiveSelected = this.$route.query.sellerTypeActiveSelected;
    }
    let index = this.category.map(object => object.enName).indexOf(this.$route.query.categorySelected);
    if (this.$route.query.categorySelected !== undefined) {
      this.categorySelected = this.$route.query.categorySelected;
      this.categoryDetail = !this.categoryDetail;
      this.showBrand(index);
    }
    if (this.$route.query.brandSelected !== undefined && this.$route.query.categorySelected !== undefined) {
      this.brandSelected = this.$route.query.brandSelected.split("--");
    }
    if (this.$route.query.priceRang !== undefined && this.$route.query.categorySelected !== undefined) {
      this.category[index].priceRang = this.$route.query.priceRang.split("--").map(Number);
    }
  },
  updated() {
  }
};
</script>

<template>
  <div class="container theForms">
    <div class="row">

      <div class="col-12 mb-3" v-if="Object.keys(myQuery).length !== 0 && myQuery.constructor === Object">
        <div class="alert alert-success text-end" role="alert" dir="ltr">
          {{ myQuery }}
        </div>
      </div>

      <div class="col-6">

        <!--Product Name-->
        <slotCard>
          <template v-slot:title>
            <p class="title">نام کالا</p>
          </template>
          <template v-slot:inputData>
            <input type="text" class="form-control" v-model="productName" placeholder="یک مقدار وارد نمایید.">
          </template>
        </slotCard>
        <!--End Product Name-->

        <!--Seller Type-->
        <slotCard>
          <template v-slot:title>
            <p class="title">نوع فروشنده</p>
          </template>
          <template v-slot:inputData>
            <div class="form-check form-check-inline" v-for="(seller,index) in sellers" :key="index">
              <input class="form-check-input" type="checkbox" :id="seller.enName" :value="seller.enName"
                     v-model="sellerType">
              <label class="form-check-label" :for="seller.enName">{{ seller.name }}</label>
            </div>
          </template>
        </slotCard>
        <!--End Seller Type-->

        <!--Product Status-->
        <slotCard>
          <template v-slot:title>
            <p class="title">وضعیت کالا</p>
          </template>
          <template v-slot:inputData>
            <div class="form-check">
              <input class="form-check-input" type="checkbox" value="" id="productStatus" v-model="productStatus">
              <label class="form-check-label" for="productStatus" @click="clearBrands">فقط کالاهای موجود</label>
            </div>
            <Transition>
              <div class="card position-relative mt-4 bg-light" v-show="productStatus">
                <div class="card-body pt-4">
                  <p class="title">انبارهای فعال</p>
                  <select class="form-select" v-model="sellerTypeActiveSelected">
                    <option selected value="All">همه</option>
                    <option v-for="(item, index) in sellerTypeActive" :key="index" :value="item.enName">
                      {{ item.name }}
                    </option>
                  </select>
                </div>
              </div>
            </Transition>
          </template>
        </slotCard>
        <!--End Product Status-->

        <!--Select Category and Brand and Price Range-->
        <slotCard>
          <template v-slot:title>
            <p class="title">دسته بندی</p>
          </template>
          <template v-slot:inputData>
            <select class="form-select" v-model="categorySelected" @change="clearCategory">
              <option value="" disabled hidden>لطفا یک دسته انتخاب کنید</option>
              <option v-for="(item, index) in category" :key="index" :value="item.enName" @click="showBrand(index)">
                {{ item.name }}
              </option>
            </select>
            <Transition>
              <section v-show="categoryDetail">
                <div class="card mb-4 position-relative mt-4 bg-light">
                  <div class="card-body pt-4">
                    <p class="title">برند</p>
                    <div v-for="(item, index) in categoryActive" :key="index">
                      <div class="form-check form-check-inline" v-for="(brand, index) in item.brands" :key="index">
                        <input class="form-check-input" type="checkbox" :id="brand.enName" :value="brand.enName"
                               v-model="brandSelected">
                        <label class="form-check-label" :for="brand.enName">{{ brand.name }}</label>
                      </div>
                    </div>
                  </div>
                </div>
                <div class="card position-relative mt-4 bg-light">
                  <div class="card-body pt-5 mx-2">
                    <p class="title">قیمت</p>
                    <div v-for="(item, index) in categoryActive" :key="index">
                      <Slider v-model="item.priceRang" />
                    </div>
                    <!--<div class="output">Data: {{ value }}</div>-->
                  </div>
                </div>
              </section>
            </Transition>
          </template>
        </slotCard>
        <!--End Select Category and Brand and Price Range-->

      </div>

      <div class="col-6">
        <div class="row">

          <!--Active Filters-->
          <slotCardHeader>
            <template v-slot:title>
              <div class="card-header">فیلترهای اعمال شده</div>
            </template>
            <template v-slot:inputData>
              <!--Filter productName-->
              <button v-if="productName !== '' && productName !== null" type="button"
                      class="btn btn-success btn-sm me-2 my-1" @click="clearFilter('productName')">
                نام کالا:
                <span><small class="badge bg-light mx-1 text-dark">{{ productName }}</small></span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
              <!--Filter sellerType-->
              <button v-if="sellerType.length !== 0" type="button" class="btn btn-success btn-sm me-2 my-1"
                      @click="clearFilter('sellerType')">
                نوع فروشنده:
                <span v-for="(item , index) in sellerType" :key="index"><small
                  class="badge bg-light mx-1 text-dark">{{ item
                  }}</small></span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
              <!--Filter productStatus-->
              <button v-if="productStatus" type="button" class="btn btn-success btn-sm me-2 my-1"
                      @click="clearFilter('productStatus')">
                <span>فقط کالاهای موجود</span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
              <!--Filter sellerTypeActiveSelected-->
              <button v-if="productStatus && sellerTypeActiveSelected.length > 0" type="button"
                      class="btn btn-success btn-sm me-2 my-1" @click="clearFilter('productStatus')">
                در انبار:
                <span><small class="badge bg-light mx-1 text-dark">{{ sellerTypeActiveSelected }}</small></span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
              <!--Filter categorySelected-->
              <button v-if="categorySelected !== '' && categorySelected.length > 0" type="button"
                      class="btn btn-success btn-sm me-2 my-1" @click="clearFilter('categorySelected')">
                در دسته:
                <span><small class="badge bg-light mx-1 text-dark">{{ categorySelected }}</small></span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
              <!--Filter brandSelected-->
              <button v-if="categorySelected.length > 0 && brandSelected.length > 0" type="button"
                      class="btn btn-success btn-sm me-2 my-1" @click="clearFilter('brandSelected')">
                برندهای:
                <span v-for="(item , index) in brandSelected" :key="index"><small
                  class="badge bg-light mx-1 text-dark">{{ item }}</small></span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
              <!--Filter priceRang-->
              <button v-if="categorySelected.length > 0 && categoryActive.length > 0" type="button"
                      class="btn btn-success btn-sm me-2 my-1" @click="clearFilter('priceRang')">
                قیمت:
                <span v-for="(item , index) in categoryActive" :key="index" dir="ltr"><small
                  class="badge bg-light mx-1 text-dark text-end">{{ item.priceRang }}</small></span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
            </template>
          </slotCardHeader>
          <!--End Active Filter-->

          <!--Operator Filters-->
          <slotCardHeader>
            <template v-slot:title>
              <div class="card-header">عملیات</div>
            </template>
            <template v-slot:inputData>
              <button type="button" class="btn btn-danger btn-sm me-2" @click="clearAllFilter">پاک کردن همه<i
                class="d-inline-flex ms-1 mdi mdi-check-all"></i></button>
            </template>
          </slotCardHeader>
          <!--End Operator Filters-->

        </div>
      </div>
    </div>
  </div>
</template>