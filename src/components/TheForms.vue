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
          enName: "businessesSeller"
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
      showPrice: false,
      priceValue: "",
      categorySelected: "",
      brandSelected: [],
      categoryDetail: false,
      // oldProductName: "",
      // oldSellerType: [],
      // oldProductStatus: false,
      // oldSellerTypeActiveSelected: "All",
      // oldCategorySelected: "",
      // oldBrandSelected: [],
      // oldPriceValue: "",

    };
  },
  watch: {
    productName: {
      immediate: true,
      handler(newVal) {
        if (newVal !== '' && newVal !== undefined) {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query, {productName: newVal.length > 0 ? newVal : undefined})
          });
        } else {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query, {productName: undefined})
          });
        }
      }
    },
    sellerType: {
      deep: true,
      handler(newVal) {
        if (newVal !== '' && newVal !== undefined) {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query, {sellerType: newVal.length > 0 ? newVal.toString().replaceAll(",", "--") : undefined})
          });
        } else {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query, {sellerType: undefined})
          });
        }
      }
    },
    productStatus: {
      immediate: true,
      handler(newVal) {
        if (newVal === false) {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query, {
              productStatus: undefined
            }, {
              sellerTypeActiveSelected: undefined
            })
          });
        } else {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query, {productStatus: newVal === true ? newVal : undefined})
          });
        }
      }
    },
    sellerTypeActiveSelected: {
      immediate: true,
      handler(newVal) {
        if (newVal === "All") {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query, {
              productStatus: undefined
            }, {
              sellerTypeActiveSelected: undefined
            })
          });
        } else {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query, {sellerTypeActiveSelected: newVal.length > 0 && newVal !== "All" ? newVal : undefined})
          });
        }
      }
    },
    categorySelected: {
      immediate: true,
      handler(newVal) {
        this.$router.push({
          path: "/",
          query: Object.assign({}, this.$route.query, {categorySelected: newVal.length > 0 ? newVal : undefined},
              {brandSelected: undefined}
          )
        });
      }
    },
    brandSelected: {
      immediate: true,
      handler(newVal) {
        this.$router.push({
          path: "/",
          query: Object.assign({}, this.$route.query,
              {categorySelected: this.categorySelected.length > 0 ? this.categorySelected : undefined},
              {brandSelected: newVal.length > 0 && this.categorySelected.length > 0 ? newVal.toString().replaceAll(",", "--") : undefined}
          )
        });
      }
    },
    priceValue: {
      immediate: true,
      handler(newVal) {
        if (newVal !== '' && newVal !== '0--100') {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query,
                {priceRang: newVal},
            )
          });
        } else if (newVal === '0--100') {
          this.$router.push({
            path: "/",
            query: Object.assign({}, this.$route.query,
                {priceRang: undefined},
                {categorySelected: this.categorySelected.length > 0 ? this.categorySelected : undefined},
                {brandSelected: this.brandSelected.length > 0 && this.categorySelected.length > 0 ? this.brandSelected.toString().replaceAll(",", "--") : undefined}
            )
          });
        }
      }
    },
    // "$route.query": {
    //   immediate: true,
    //   deep: true,
    //   handler(newVal, oldVal) {
    //     let paramsChangeProductName, paramsChangeSellerType, paramsChangeProductStatus,
    //         paramsChangeSellerTypeActiveSelected, paramsChangeCategorySelected, paramsChangeBrandSelected,
    //         paramsChangePriceValue
    //     // if (oldVal.productName !== undefined) {
    //     //   paramsChangeProductName = oldVal.productName
    //     // }
    //     // if (oldVal.sellerType !== undefined) {
    //     //   paramsChangeSellerType = oldVal.sellerType
    //     // }
    //     // paramsChangeProductStatus = oldVal.productStatus
    //     // paramsChangeSellerTypeActiveSelected = oldVal.sellerTypeActiveSelected
    //     // paramsChangeCategorySelected = oldVal.categorySelected
    //     // paramsChangeBrandSelected = oldVal.brandSelected
    //     // paramsChangePriceValue = oldVal.priceRang
    //     //
    //     // console.log(paramsChangeProductName)
    //     // console.log(paramsChangeSellerType)
    //     // console.log(paramsChangeProductStatus)
    //     // console.log(paramsChangeSellerTypeActiveSelected)
    //     // console.log(paramsChangeCategorySelected)
    //     // console.log(paramsChangeBrandSelected)
    //     // console.log(paramsChangePriceValue)
    //
    //     // console.log(this.$route.from.fullPath)
    //     // if (oldVal !== undefined) {
    //     //   if (newVal.productName !== oldVal.productName) {
    //     //     this.productName = oldVal.productName
    //     //   }
    //     // }
    //
    //     // if (this.$route.query.productName !== '') {
    //     //   this.productName = oldVal.productName || ''
    //     // }
    //     // if (this.$route.query.sellerType !== undefined) {
    //     //   this.sellerType = this.$route.query.sellerType.split("--")
    //     // }
    //     // this.productStatus = this.$route.query.productStatus
    //   }
    //
    //   // if (this.$route.query.productName && value.productName !== '') {
    //   //   this.productName = value.productName || ''
    //   // }
    //   // if (value.sellerType !== undefined && value.sellerType.length > 0) {
    //   //   this.sellerType = value.sellerType.split("--") || []
    //   //   console.log(this.sellerType)
    //   // }
    // },
    // "$route.query.productName": {
    //   handler(newVal, oldVal) {
    //     if (oldVal !== undefined) {
    //       this.oldProductName = oldVal
    //       console.log(this.oldProductName)
    //     }
    //   }
    // },
    // "$route.query.sellerType": {
    //   handler(newVal, oldVal) {
    //     if (oldVal !== undefined) {
    //       this.oldSellerType = oldVal
    //       console.log(this.oldSellerType)
    //     }
    //   }
    // },
    // "$route.query.productStatus": {
    //   handler(newVal, oldVal) {
    //     if (oldVal !== undefined) {
    //       this.oldProductStatus = oldVal
    //       console.log(this.oldProductStatus)
    //     }
    //   }
    // },
    // "$route.query.sellerTypeActiveSelected": {
    //   handler(newVal, oldVal) {
    //     if (oldVal !== undefined) {
    //       this.oldSellerTypeActiveSelected = oldVal
    //       console.log(this.oldSellerTypeActiveSelected)
    //     }
    //   }
    // },
    // "$route.query.categorySelected": {
    //   handler(newVal, oldVal) {
    //     if (oldVal !== undefined) {
    //       this.oldCategorySelected = oldVal
    //       console.log(this.oldCategorySelected)
    //     }
    //   }
    // },
    // "$route.query.brandSelected": {
    //   handler(newVal, oldVal) {
    //     if (oldVal !== undefined) {
    //       this.oldBrandSelected = oldVal
    //       console.log(this.oldBrandSelected)
    //     }
    //   }
    // },
    // "$route.query.priceRang": {
    //   handler(newVal, oldVal) {
    //     if (oldVal !== undefined) {
    //       this.oldPriceValue = oldVal
    //       console.log(this.oldPriceValue)
    //     }
    //   }
    // },
    // '$route.query': {
    //   immediate: true,
    //   handler(newVal, oldVal) {
    //     // this.$router.replace({name: "home", query: oldVal})
    //     // console.log(oldVal)
    //     // console.log(newVal)
    //     // make actions with newVal.page
    //   }
    // }
  },
  computed: {
    sellerTypeActive() {
      return this.sellers.filter(item => item.status === true);
    },
    categoryActive() {
      return this.category.filter(item => item.status === true);
    },
    myQuery() {
      this.categoryActive.forEach((element) => {
        this.priceValue = element.priceRang.toString().replaceAll(",", "--");
      });
      return this.$route.query;
    },
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
    clearSellerType(id) {
      this.sellerType.splice(id, 1);
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
          this.showPrice = false;
          break;
        case "brandSelected":
          this.brandSelected = [];
          break;
        case "priceRang":
          this.category.filter(item => item.priceRang = [0, 100]);
          this.showPrice = false;
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
      delete this.$route.query.productName
      delete this.$route.query.sellerType
      delete this.$route.query.productStatus
      delete this.$route.query.sellerTypeActiveSelected
      delete this.$route.query.categorySelected
      delete this.$route.query.brandSelected
      delete this.$route.query.priceRang
      window.history.pushState({}, document.title, "/");
    }
  },
  mounted() {
    if (this.$route.query.productName !== undefined) {
      this.productName = this.$route.query.productName;
    }
    if (this.$route.query.sellerType !== undefined) {
      this.sellerType = this.$route.query.sellerType.split("--");
      // this.sellerType = this.$route.query.sellerType.split(",");
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
      // this.brandSelected = this.$route.query.brandSelected.split(",");
    }
    if (this.$route.query.priceRang !== undefined && this.$route.query.categorySelected !== undefined) {
      this.showPrice = true;
      this.category[index].priceRang = this.$route.query.priceRang.split("--").map(Number);
    }
  },
  updated() {
    // if (this.productName !== undefined) {
    //   this.productName = this.$route.query.productName
    // }
    // if(this.$route.query.sellerType.length > 0){
    // console.log(1111)
    //
    //
    // }
    // if (this.sellerType !== undefined) {
    //   // this.sellerType = []
    //   // this.sellerType = this.$route.query.sellerType.split("--")
    // }
    // if(this.oldProductName !== this.$route.query.productName){
    //   this.productName = this.oldProductName
    // }
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
              <slotCard customClass="true" v-show="productStatus">
                <template v-slot:title>
                  <p class="title">انبارهای فعال</p>
                </template>
                <template v-slot:inputData>
                  <select class="form-select" v-model="sellerTypeActiveSelected">
                    <option selected value="All">همه</option>
                    <option v-for="(item, index) in sellerTypeActive" :key="index" :value="item.enName">
                      {{ item.name }}
                    </option>
                  </select>
                </template>
              </slotCard>
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
                <slotCard customClass="true">
                  <template v-slot:title>
                    <p class="title">برند</p>
                  </template>
                  <template v-slot:inputData>
                    <div v-for="(item, index) in categoryActive" :key="index">
                      <div class="form-check form-check-inline" v-for="(brand, index) in item.brands" :key="index">
                        <input class="form-check-input" type="checkbox" :id="brand.enName" :value="brand.enName"
                               v-model="brandSelected">
                        <label class="form-check-label" :for="brand.enName">{{ brand.name }}</label>
                      </div>
                    </div>
                  </template>
                </slotCard>
                <slotCard customClass="true">
                  <template v-slot:title>
                    <p class="title">قیمت</p>
                  </template>
                  <template v-slot:inputData>
                    <div class="mt-4 mx-2" v-for="(item, index) in categoryActive" :key="index">
                      <Slider v-model="item.priceRang" @change="showPrice = true"/>
                    </div>
                  </template>
                </slotCard>
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
              <button v-if="productName !== '' && productName !== undefined" type="button"
                      class="btn btn-success btn-sm me-2 my-1" @click="clearFilter('productName')">
                نام کالا:
                <span><small class="badge bg-light mx-1 text-dark">{{ productName }}</small></span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
              <!--Filter sellerType-->
              <button v-if="sellerType.length !== 0" type="button" class="btn btn-success btn-sm me-2 my-1">
                نوع فروشنده:
                <span v-for="(item , index) in sellerType" :key="index">
                  <small class="badge bg-light mx-1 text-dark">{{ item }} <span class="d-inline-flex ms-1 mdi mdi-close"
                                                                                @click="clearSellerType(index)"></span></small>
                </span>
                <span class="d-inline-flex ms-1 mdi mdi-close" @click.self="clearFilter('sellerType')"></span>
              </button>
              <!--Filter productStatus-->
              <button v-if="productStatus" type="button" class="btn btn-success btn-sm me-2 my-1"
                      @click="clearFilter('productStatus')">
                <span>فقط کالاهای موجود</span>
                <span class="d-inline-flex ms-1 mdi mdi-close"></span>
              </button>
              <!--Filter sellerTypeActiveSelected-->
              <button v-if="productStatus && sellerTypeActiveSelected.length > 0 && sellerTypeActiveSelected !== 'All'"
                      type="button"
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
              <button v-if="categorySelected.length > 0 && categoryActive.length > 0 && showPrice" type="button"
                      class="btn btn-success btn-sm me-2 my-1" @click="clearFilter('priceRang')">قیمت:
                <span v-for="(item , index) in categoryActive" :key="index" dir="ltr">
                  <small class="badge bg-light mx-1 text-dark text-end">{{ item.priceRang }}</small>
                </span>
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