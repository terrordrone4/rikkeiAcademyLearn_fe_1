<template>
  <div id="root">
    <div class="header"> <!-- top-bar -->
      <div class="header-inner">
        <a href="/" class="logo">Free 3D</a>

        <div class="nav-search-bar">
          <input type="text" class="search-bar" placeholder="search 3d models ...">
        </div>

        <div class="nav-links">
          <a href="/free-3d-model" class="each-nav-link">Free 3D model</a>
          <a href="/premium-3d-model" class="each-nav-link">Premium 3D model</a>
        </div>'
        '
        <div class="login-register-group">
          <div class="register login-register">

            <div class="login-register-button" @click="showLoginModal">
              Create Free Account
            </div>

          </div>
          <div class="inbetween">
            or
          </div>
          <div class="login login-register">
            <div class="login-register-button" @click="showLoginModal">
              Login
            </div>
            <div class="login-dropdown">
              <div class="triangle"></div>
              <modal v-show="isLoginModalVisible" @close="hideLoginModal" />
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="main">
      <div class="model-type-container">
        <div class="model-type-group">
          <a href="3d-model/blender" class="small-icon">
            <div class="image">
              <img src="../assets/image/blender3179.jpg">
            </div>
            <div class="label-container">
              <div class="label">Blender Models</div>
            </div>
          </a>
          <a href="3d-model/fbx" class="small-icon">
            <div class="image">
              <img src="../assets/image/fbx.png">
            </div>
            <div class="label-container">
              <div class="label">FBX Models</div>
            </div>
          </a>
          <a href="3d-model/cinema-4d" class="small-icon">
            <div class="image">
              <img src="../assets/image/cinema-4d-512-icon.png">
            </div>
            <div class="label-container">
              <div class="label">Cinema 4D Models</div>
            </div>
          </a>
          <a href="3d-model/Maya" class="small-icon">
            <div class="image">
              <img src="../assets/image/Maya.png">
            </div>
            <div class="label-container">
              <div class="label">Maya Models</div>
            </div>
          </a>
          <a href="3d-model/3d-max" class="small-icon">
            <div class="image">
              <img src="../assets/image/3d-max.png">
            </div>
            <div class="label-container">
              <div class="label">3D Max Models</div>
            </div>
          </a>
          <a href="3d-model/obj" class="small-icon">
            <div class="image">
              <img src="../assets/image/obj-icon.png">
            </div>
            <div class="label-container">
              <div class="label">Obj Models</div>
            </div>
          </a>

          <a href="3d-model/rigged" class="small-icon">
            <div class="image">
              <img src="../assets/image/rigged.png">
            </div>
            <div class="label-container">
              <div class="label">Obj Models</div>
            </div>
          </a>

          <a href="3d-model/animated" class="small-icon">
            <div class="image">
              <img src="../assets/image/man-dancing.png">
            </div>
            <div class="label-container">
              <div class="label">Obj Models</div>
            </div>
          </a>

          <a href="3d-model/low-poly" class="small-icon">
            <div class="image">
              <img src="../assets/image/2560px-LowPoly_Sphere_20.stl.png">
            </div>
            <div class="label-container">
              <div class="label">Obj Models</div>
            </div>
          </a>
        </div>
      </div>

      <div class="category-container"> <!-- @scroll="onScroll" -->
        <div class="categ" v-for="category_block in category_blocks" :key="category_block.id">
          <div class="desc-block">
            <div class="category-title">
              <span class="category-icon">
              </span>
              <a href="/">
                Some Title
              </a>
            </div>

            <div class="category-context">
              blasdn gkasmdkhk,b lsdlamfl,,g
              kamsdk b,b,as,dals,dl,,,g,hm bbkkqwe
              iiyoypk osdnsflasmgl wowkepwt ippopipio
              hghghtyhf jjsjjg
              asdkasdlasmflksamglkmg askdmadmaw
              jfngjn jgnaslksgklasgkamg wkmwmfg fs asd
            </div>
          </div>
          <div class="example-block" v-for="example_block in category_block.example_blocks" :key="example_block.id">
            <div class="content-wrapper">
              <a href="/">
                <img :src="example_block.image">
              </a>
            </div>
            <div class="info-wrapper">
              <div class="title">
                Living Room
              </div>
              <div class="format">
                .blend .fbx .obj
              </div>
              <div class="footer">
                <span class="price">Free</span>
                <span class="stats">
                  <span class="download-count">
                    103,720
                  </span>
                </span>
              </div>
            </div>
          </div>

        </div>
      </div>




    </div>
    <div class="footer"></div>
  </div>
</template>

<script>


import modal from './LoginModal.vue';

export default {
  name: 'HomePage',

  components: {
    modal,
  },

  props: {
  },

  data: function () {
    return {
      isLoginModalVisible: false,

      category_blocks_counter: 0,
      category_blocks: [{
        id: 'category_blocks-0',
        example_blocks_counter: 0,
        example_blocks: [{
          id: 'example-block-0',
          image: this.getRandomImage(),
        }],
      }],

      images: [
        "../image/living-room.png",
        "../image/cyclops-subnautica.png",
        "../image/low-poly-f1-car.png",
      ],

      CACHE_AMOUNT_ALLOW_MAX: 8,
      ELEMENT_HEIGHT: 300,

      elementHidenOnTop: 0,
      elementHidenBellow: 0,
    }
  },

  computed: {
    isCategoryCountExcedding: function () {
      return true;
    }
  },

  methods: {
    onScroll(element) {
      //const { scrollTop, offsetHeight, scrollHeight } = element.target;
      
      const { scrollTop } = element.target;

      this.elementHidenOnTopCount = this.getHiddenElementOnTopCount(scrollTop);

      // if ((scrollTop + offsetHeight) >= scrollHeight) {
      //   console.log('bottom!')
      // }

      if (this.elementHidenOnTopCount > this.CACHE_AMOUNT_ALLOW_MAX) {
        this.disposeScrollElement(0, this.elementHidenOnTopCount - this.CACHE_AMOUNT_ALLOW_MAX);
      }
    },

    getHiddenElementCount(scrollTop) {
      return scrollTop / this.ELEMENT_HEIGHT;
    },

    disposeScrollElement(startIndex, endIndex) {
      for (let i = 0; i < this.category_blocks.length; i++) {
        if (i < startIndex) {
          continue;
        }
        if (i > endIndex) {
          break;
        }
        this.dispose(this.category_blocks[i]);
      }
    },

    dispose(targetCategBlock) {

      targetCategBlock.example_blocks.forEach(example_block => {
        example_block.image = "";
      });
    },

    showLoginModal() {
      this.isLoginModalVisible = true;
    },

    hideLoginModal() {
      this.isLoginModalVisible = false;
    },

    cloneExampleBlock(cloneAmount, targetCategBlock) {

      for (let i = 0; i < cloneAmount; i++) {
        targetCategBlock.example_blocks_counter++;
        targetCategBlock.example_blocks.push({
          id: `example-block-${targetCategBlock.example_blocks_counter}`,
          image: this.getRandomImage(),
        });

      }
    },

    cloneCategoryBlock(cloneAmount) {
      for (let i = 0; i < cloneAmount; i++) {
        this.category_blocks_counter++;
        this.category_blocks.push({

          id: `category-${this.category_blocks_counter}`,

          example_blocks_counter: 0,
          example_blocks: [{
            id: 'example-block-0',
          }],

        });
        let newCategBlock = this.category_blocks[this.category_blocks.length - 1]
        this.cloneExampleBlock(4, newCategBlock);
      }
    },

    getRandomImage() {
      let imageAvailabeCount = this.images.length;
      let randomElementId = Math.floor(Math.random() * imageAvailabeCount);
      return this.images[randomElementId];
    }
  },
  mounted() {
    console.log("mounted" + this.category_blocks);
    console.log("mounted" + this.category_blocks.length);

    let lastCategBlock = this.category_blocks[this.category_blocks.length - 1];
    this.cloneExampleBlock(4, lastCategBlock);

    this.cloneCategoryBlock(500);
  },
}
</script>

<style scoped>
@import '../assets/css/homepage.css';
</style>
