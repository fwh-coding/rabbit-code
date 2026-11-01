<script setup>
import { ref, onMounted } from "vue";
import { getCategoryFilterAPI } from "@/apis/category";
import { useRoute } from "vue-router";
// 获取面包屑导航数据
const route = useRoute();
const filterData = ref({});
const getFilterData = async () => {
    const res = await getCategoryFilterAPI(route.params.id);
    filterData.value = res.result;
};
onMounted(() => {
    getFilterData();
});
</script>

<template>
    <div class="container">
        <!-- 面包屑 -->
        <div class="bread-container">
            <el-breadcrumb separator=">">
                <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
                <el-breadcrumb-item :to="{ path: `/category/${filterData.parentId}` }">{{ filterData.parentName }}
                </el-breadcrumb-item>
                <el-breadcrumb-item>{{ filterData.name }}</el-breadcrumb-item>
            </el-breadcrumb>
        </div>
        <div class="sub-container">
            <el-tabs>
                <el-tab-pane label="最新商品" name="publishTime"></el-tab-pane>
                <el-tab-pane label="最高人气" name="orderNum"></el-tab-pane>
                <el-tab-pane label="评论最多" name="evaluateNum"></el-tab-pane>
            </el-tabs>
            <div class="body">
                <!-- 商品列表-->
            </div>
        </div>
    </div>
</template>
