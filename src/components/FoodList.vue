<template>
    <div class="mb-6 overflow-y-auto scrollable" style="height: 452px;">
        <!-- 類別名稱 -->
        <h2 class="text-2xl font-semibold text-gray-700 text-center mb-4">{{ foodItem.category }}</h2>
        <ul class="space-y-6">
            <li v-for="item in foodItem.foods" :key="item.name"
                class="flex flex-col md:flex-row justify-between items-start md:items-center border-b pb-4">
                <!-- 食物名稱 -->
                <span class="text-lg font-semibold text-gray-800">
                    {{ item.name }}
                </span>
                <!-- 每公克卡路里 -->
                <div>
                    <label class="block text-sm text-gray-600 mb-1">每公克卡路里：</label>
                    <span class="text-gray-800 font-medium">{{ item.caloriesPerGram }} cal</span>
                </div>
                <!-- 公克/卡路里資訊 -->
                <div
                    class="flex flex-col md:flex-row items-start md:items-center space-y-2 md:space-y-0 md:space-x-6 mt-2 md:mt-0">
                    <!-- 公克輸入框 -->
                    <div>
                        <label class="block text-sm text-gray-600 mb-1">重量 (公克)：</label>
                        <input type="number" v-model.number="item.weight" placeholder="輸入重量"
                            class="w-32 px-3 py-2 border border-gray-300 rounded focus:outline-none focus:ring focus:ring-blue-300 appearance-none">
                    </div>
                </div>
            </li>
        </ul>
    </div>
</template>

<script>
export default {
    props: {
        foodItem: {
            type: Object,
            require: true
        }
    },
    data() {
        return {

        }
    },
}
</script>