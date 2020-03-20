<template>
  <div class="addTag">
    <div class="navBar">
      <Icon class="leftIcon" name="left" @click="goBack" />
      <span class="title">
        <strong>添加标签</strong>
      </span>
      <span class="rightIcon" />
    </div>
    <ul class="current">
      <li v-for="tag in tagNameList" :key="tag.id" @click="addTag(tag)">
        <Icon class="item" :name="tag.name" />
        {{ tag.name }}
      </li>
      <li>
        <div @click="createTag"><Icon name="新建" />自定义标签</div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { Component, Prop } from "vue-property-decorator";
import { mixins } from "vue-class-component";
import TagHelper from "../mixins/TagHelper";
import recordTypeList from "@/constants/recordTypeList";
import Nav from "@/components/Nav.vue";

@Component
export default class Tags extends mixins(TagHelper) {
  tagNameList = [
    { id: "1", name: "服饰" },
    { id: "2", name: "餐饮" },
    { id: "3", name: "住房" },
    { id: "4", name: "交通" },
    { id: "5", name: "礼物" },
    { id: "6", name: "零食" },
    { id: "7", name: "工资" },
    { id: "8", name: "红包" },
    { id: "9", name: "宠物" },
    { id: "10", name: "彩票" },
    { id: "11", name: "日用" },
    { id: "12", name: "社交" },
    { id: "13", name: "书籍" },
    { id: "14", name: "数码" },
    { id: "15", name: "蔬菜" },
    { id: "16", name: "水果" },
    { id: "17", name: "通讯" },
    { id: "18", name: "医疗" },
    { id: "19", name: "购物" },
    { id: "20", name: "娱乐" }
  ];

  nameList = this.$store.state.tagList.map((t: any) => t.name);

  addTag(tag: any) {
    if (this.nameList.indexOf(tag.name) >= 0) {
      window.alert("该标签已存在");
      return;
    }
    this.$store.commit("createTag", tag.name);
    this.$router.back();
  }

  goBack() {
    this.$router.back();
  }
}
</script>

<style lang="scss" scoped>
.addTag {
  > .navBar {
    background: white;
    text-align: center;
    font-size: 16px;
    padding: 12px 16px;
    background: white;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  > .current {
    background: white;
    margin-top: 8px;
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
        background: yellow;
      }
    }
  }
}
</style>
