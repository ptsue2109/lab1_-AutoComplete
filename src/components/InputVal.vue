<template>
  <div>
    <div class="container">
      <img src="@/assets/search.svg" alt="" />
      <div class="tag-container">
        <ul>
          <li v-for="item in selectedItem" :key="item.id">
            {{ item }}
            <img
              @click="removeTag(item)"
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAEAAAABACAYAAACqaXHeAAAABmJLR0QA/wD/AP+gvaeTAAADBElEQVR4nO3aTahVVRjG8d+xm5eMUMpKSL0VQgQJQU36nDRwZBI3GwURFEUGDnLgsMRo0CgICyVo1CjIKIiKosiaZEWDCpJCrEAuJZl9ErfdYDm4HL3nvnvtdfY94vrDmu31nOd5z15nv2vtQ6VSqVQqlUqlUjkfGRTUWo+tmMEJvI0vC2mvxXZswCm8i8OFtIuwG/+gGRoHsLKj9m34+SzaB3FJR+0iPOhMcwvHvg7aV2FuhPbBDtrFOGJ0ARrck6E7wFsB7eu72e/GmkVMDY/juKyl9kNB7ZziFiNagAavtNDdiJNB3dsL5OjEd+JFiHxbA7wT1DuO6XJR8nhCvACRpfBIC72Hy0bJ40J8psxSuBq/BXVeVbaP6cQm8TXbYPYsGgOpeYrM/xarx5Ymk/vECzCHK4bmPx6c+yduHG+UfPbJWwrXSC1uZN4DPeTIZlq734NZrMAHwetf6C9KPpvwq/hTYW/w2k9NwCMvyr3id0FknJCWyTnF88qE/w/bevZehGlpz961AHv6Nl6SGfwiP/x7uKB314XZKt3GbcP/gMuXwe9YeEn7AtzSh7EVPXzGxdKxVlsmtttry8vy1v/fuGkZ/BZlu25PgKPanyRNDNeKd4SjxhsmaNsbZQqfKNMINdjVr/3uPKNc+Ab/4o5eE3TgLsyLBTvU4tofnXmGMHGsxU9igb6X3uw8Hby+wfsmuDMc4HWxIPO48/S8KXwcnNfgyV7SZLBTPMRTQ3M3iO8Z5rFlvFHac4N0VhcJcFg6SR5mNji/kYo1M7Y0LVmFb8SM/47rRmjtD+o0+MiE/B48K2760SW0VuGrFno7y0Zpz2rxW/9NsY5uM/4Kah4pFyWPLWJG53BlC93HgrqNZX5Bsm0RU8Pj7gzt14Laazol6MhGS3dy+zO1L8WxJbSXfQnAixY3+Ll0IJLLzfhjhP79HbSLsRLPSRuWheY+xLoC+rdK5wILtU9iRwHtovvsdZLZi/A1viioPSX9E2S91AQdkt4lViqVSqVSqVQqlUoW/wNjPM9qeBIcrwAAAABJRU5ErkJggg=="
            />
          </li>
        </ul>
      </div>
      <input
        placeholder="Nhập tên cần tìm kiếm"
        v-model="search"
        @input="filterList"
        type="text"
        name="item-input"
        multiple
      />
    </div>
    <div class="dropdown">
      <div
        class="dropdown__item"
        v-for="item in listFilter"
        :key="item.code"
        @click="addTag(item.name)"
      >
        {{ item.name }}
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "InputVal",
  props: {
    listArray: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      search: "",
      listFilter: [],
      selectedItem: [],
    };
  },
  methods: {
    filterList() {
      if (this.search.length > 0) {
        this.listFilter = [...this.listArray];
        this.listFilter = this.listFilter.filter((item) =>
          item.name.toLowerCase().includes(this.search.toLowerCase())
        );
      } else {
        this.listFilter = [];
      }
    },
    addTag(itemName) {
      console.log(itemName);
      if (!this.selectedItem.includes(itemName)) {
        this.selectedItem.push(itemName);
      } else {
        this.listFilter = [];
        alert("Địa chỉ đã được chọn");
      }
      this.search = "";
    },
    removeTag(itemName) {
      const rs = window.confirm(`Xóa ${itemName}`);
      if (rs) {
        this.selectedItem = this.selectedItem.filter(
          (item) => item !== itemName
        );
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.container {
  height: auto;
  border-radius: 4px;
  border: 1px solid #dbdbdb;
  background: rgba(230, 249, 255, 0.2);
  margin-left: auto;
  margin-right: auto;
  display: flex;
  align-items: center;
  flex-wrap: wrap;
  width: 450px;

  & img {
    width: 20px;
    height: 20px;
    margin: 12.5px 4px 12.5px 10px;
  }
}
.tag-container {
  display: flex;
  & ul {
    display: flex;
    padding: 0px;
    text-align: left;
    flex-wrap: wrap;
  }

  & li {
    background: #f0f4f8;
    border: 1px solid #dcdcdc;
    border-radius: 4px;
    padding: 4px 0px 4px 8px;
    list-style: none;
    margin: 8px 4px 8px 0px;
    font-family: "Noto Sans";
    font-size: 14px;
    color: #627d98;
    line-height: 20px;
  }

  & img {
    width: 15px;
    height: 15px;
    margin-top: auto;
    margin-bottom: auto;
    margin-left: 0px;
    margin-right: 0px;
    &:hover {
      cursor: pointer;
    }
  }
}
input {
  flex: 1;
  height: 48px;
  border: none;
  background: rgba(230, 249, 255, 0.2);
  font-family: "Noto Sans";
  font-size: 14px;
  width: 120px;
  &:focus {
    outline: none;
  }
  &.checkbox {
    width: 13px;
  }
}

.dropdown {
  display: flex;
  flex-direction: column;
  font-family: "Noto Sans";
  margin-left: auto;
  margin-right: auto;
  width: 400px;
  height: 126px;
  overflow: auto;
  &__item {
    text-align: left;
    padding: 10px;
    gap: 10px;
    color: #486581;
    background-color: #f1f5f8;
    &:first-child {
      border-radius: 4px 4px 0px 0px;
    }
    &:last-child {
      border-radius: 0px 0px 4px 4px;
    }

    &:hover {
      cursor: pointer;
      color: #ffffff;
      background-color: #617d98;
    }
  }
}
</style>
