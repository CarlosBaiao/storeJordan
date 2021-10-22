<template>
  <div class="category-menu">
    <ul>
      <li
        v-for="category in categoryList"
        :key="category.id"
        @click="onCategoryClick(category.id)"
        :class="{ active: isActive(category.id) }"
      >
        <component :is="category.icon" />
        <p>{{ category.label }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import Cap from "../assets/images/cap.svg";
import Shirt from "../assets/images/shirt.svg";
import Jacket from "../assets/images/jacket.svg";
import Sneakers from "../assets/images/sneakers.svg";

export default {
  name: "CategoryMenu",
  components: {
    Cap,
    Shirt,
    Jacket,
    Sneakers,
  },
  data() {
    return {
      categoryList: [
        { label: "Caps", icon: "Cap", id: "cap" },
        { label: "T-shirts", icon: "Shirt", id: "shirt" },
        { label: "Jackets", icon: "Jacket", id: "jacket" },
        { label: "Sneakers", icon: "Sneakers", id: "sneakers" },
      ],
      selectedCategory: "",
    };
  },
  mounted() {
    this.onCategoryClick('cap')
  },
  methods: {
    onCategoryClick(id) {
      this.selectedCategory = id;
      this.$store.dispatch('changeCategory', id)

    },
    isActive(id) {
      return this.selectedCategory == id;
    },
  },
};
</script>

<style scoped lang="less">
.category-menu {
  background: @light-grey;
  height: 100px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 10px;

  ul {
    list-style: none;
    padding: 0;
    display: flex;
    height: 100%;

    li {
      display: flex;
      width: 100px;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      margin: 0 50px;
      cursor: pointer;
      color: @dark-grey;

      p {
        margin: 0;
        font-size: 18px;
        font-weight: 500;
      }

      svg {
        path {
          fill: @dark-grey;
        }
      }

      &.active {
        background: @light-blue;
        border-radius: 8px;
        color: black;

        svg {
          path {
            fill: black;
          }
        }
      }
    }
  }

  @media @tablets {
    background: white;

    ul {
      li {
        background: @light-blue;
        border: 1px solid @blue;
        border-radius: 8px;
        width: 100px;
        margin: 0 10px;

        &.active {
          background: @blue;
          color: white;

          svg {
            path {
              fill: white;
            }
          }
        }
      }
    }
  }

  @media @smartphones {
    ul {
      margin: 20px;
      overflow: scroll;

      li {
        min-width: 100px;
        p {
          font-size: 15px;
        }

        &.active {
          background: @blue;
          color: white;

          svg {
            path {
              fill: white;
            }
          }
        }
      }
    }
  }
}
</style>
