<template>
  <div class="tags">
    <div class="new">
      <button>
        <router-link to="/addtag">新增标签</router-link>
      </button>
    </div>
    <ul class="current">
      <li v-for="tag in tagList" :key="tag.id" @click="toggle(tag)">
        <Icon
          class="item"
          :name="tag.name"
          v-if="tagNameList.indexOf(tag.name) >= 0"
          :class="{ selected: selectedTags.indexOf(tag) >= 0 }"
        />
        <Icon class="item" v-else name="自定义" :class="{ selected: selectedTags.indexOf(tag) >= 0 }" />
        <span>{{ tag.name }}</span>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop } from "vue-property-decorator";
import { mixins } from "vue-class-component";
import TagHelper from "../../mixins/TagHelper";
import recordTypeList from "@/constants/recordTypeList";
import router from "../../router/index";

@Component
export default class Tags extends mixins(TagHelper) {
  selectedTags: string[] = [];
  tagNameList = [
    "工资",
    "交通",
    "红包",
    "住房",
    "运动",
    "娱乐",
    "医疗",
    "通讯",
    "数码",
    "书籍",
    "水果",
    "蔬菜",
    "社交",
    "日用",
    "汽车",
    "礼物",
    "零食",
    "办公",
    "购物",
    "服饰",
    "宠物",
    "彩票",
    "餐饮",
    "宠物"
  ];

  get tagList() {
    return this.$store.state.tagList;
  }
  created() {
    this.$store.commit("fetchTags");
  }
  toggle(tag: string) {
    const index = this.selectedTags.indexOf(tag);
    if (index >= 0) {
      this.selectedTags.splice(index, 1);
    } else {
      this.selectedTags.push(tag);
    }
    this.$emit("update:value", this.selectedTags);
  }
}
</script>

<style lang="scss" scoped>
.tags {
  background: white;
  font-size: 14px;
  padding: 12px;
  flex-grow: 1;
  display: flex;
  flex-direction: column-reverse;
  > .current {
    display: flex;
    flex-wrap: wrap;
    > li {
      background: transplate;
      $h: 60px;
      height: $h;
      line-height: $h;
      padding: 12px 16px 16px 16px;
      margin-right: 8px;
      margin-top: 12px;
      margin-bottom: -8px;
      position: relative;
      display: flex;
      justify-content: center;
      align-items: center;
      > .item {
        border-radius: 4px;
        position: absolute;
        height: 28px;
        width: 28px;
        margin-top: -24px;
        margin-bottom: -24px;
        &.selected {
          background: #f8fc19;
        }
      }
    }
  }
  > .new {
    padding-top: 16px;
    button {
      background: transparent;
      border: none;
      color: #999;
      border-bottom: 1px solid;
      padding: 0 4px;
    }
  }
}
</style>
