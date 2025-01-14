<template>
    <div class="flex items-center justify-center min-h-screen bg-gray-100">
        <div class="w-full max-w-3xl px-6">
            <!-- 熱量計算器標題 -->
            <h1 class="text-3xl font-bold text-gray-800 text-center mb-6">熱量計算器</h1>

            <!-- 包裹子組件的白色框 -->
            <div class="p-6 bg-white rounded-lg shadow">
                <!-- FoodList 子組件 -->
                <FoodList :foodItem="foodCategories[currentIndex]" @update-total="totalCalories" ref="scrollable" />

                <!-- Buttons -->
                <div class="flex justify-between space-x-4 mb-6">
                    <button @click="doReset"
                        class="w-full bg-red-500 text-white px-4 py-2 rounded hover:bg-red-600 transition">
                        RESET
                    </button>
                    <button @click="doNext"
                        class="w-full bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-600 transition">
                        NEXT
                    </button>
                </div>

                <!-- Total Calories -->
                <h2 class="text-center text-xl font-bold text-gray-700">
                    總熱量: {{ total === 0 ? total : total.toFixed(2) }} cal
                </h2>
            </div>
        </div>
    </div>
</template>




<script>
import FoodList from './FoodList.vue';
export default {
    components: {
        FoodList,
    },
    data() {
        return {
            currentIndex: 0,
            total: 0,
            foodCategories: [
                {
                    category: "碳水化合物",
                    foods: [
                        { name: "糙米", caloriesPerGram: 1.11, weight: "" },
                        { name: "白飯", caloriesPerGram: 1.30, weight: "" },
                        { name: "地瓜", caloriesPerGram: 0.86, weight: "" },
                        { name: "燕麥片", caloriesPerGram: 3.89, weight: "" },
                        { name: "馬鈴薯", caloriesPerGram: 0.77, weight: "" },
                        { name: "藜麥", caloriesPerGram: 1.20, weight: "" },
                        { name: "貝果", caloriesPerGram: 2.50, weight: "" },
                        { name: "土司", caloriesPerGram: 2.40, weight: "" },
                        { name: "全麥麵包", caloriesPerGram: 2.60, weight: "" },
                        { name: "蘋果", caloriesPerGram: 0.52, weight: "" },
                        { name: "香蕉", caloriesPerGram: 0.89, weight: "" },
                        { name: "西蘭花", caloriesPerGram: 0.34, weight: "" },
                    ]
                },
                {
                    category: "蛋白質",
                    foods: [
                        { name: "雞胸肉", caloriesPerGram: 1.65, weight: "" },
                        { name: "豬里肌", caloriesPerGram: 2.50, weight: "" },
                        { name: "牛肉", caloriesPerGram: 2.50, weight: "" },
                        { name: "鮭魚", caloriesPerGram: 2.08, weight: "" },
                        { name: "鯖魚", caloriesPerGram: 2.00, weight: "" },
                        { name: "蝦仁", caloriesPerGram: 0.99, weight: "" },
                        { name: "希臘優格", caloriesPerGram: 0.59, weight: "" },
                        { name: "雞蛋", caloriesPerGram: 1.55, weight: "" },
                        { name: "豆腐", caloriesPerGram: 0.76, weight: "" },
                        { name: "蛋白粉", caloriesPerGram: 4.00, weight: "" },
                        { name: "鷹嘴豆", caloriesPerGram: 1.64, weight: "" },
                    ]
                },
                {
                    category: "油脂",
                    foods: [
                        { name: "橄欖油", caloriesPerGram: 9.00, weight: "" },
                        { name: "綜合堅果", caloriesPerGram: 5.85, weight: "" },
                        { name: "牛油果", caloriesPerGram: 1.60, weight: "" },
                        { name: "杏仁", caloriesPerGram: 5.75, weight: "" },
                        { name: "核桃", caloriesPerGram: 6.50, weight: "" },
                        { name: "腰果", caloriesPerGram: 5.53, weight: "" },
                        { name: "花生醬", caloriesPerGram: 5.90, weight: "" },
                        { name: "芝麻醬", caloriesPerGram: 5.70, weight: "" },
                    ]
                }
            ]
        }
    },
    watch: {
        foodCategories: {
            handler: "totalCalories",
            deep: true
        }
    },
    methods: {
        doNext() {
            if (this.currentIndex < this.foodCategories.length - 1) {
                this.currentIndex++;
            } else {
                this.currentIndex = 0;
            }
            this.$refs.scrollable.$el.scrollTop = 0
        },
        doReset() {
            this.foodCategories.forEach(category => {
                category.foods.forEach(food => {
                    food.weight = ""
                })
            })
            this.$refs.scrollable.$el.scrollTop = 0
            this.currentIndex = 0;
            this.total = 0;
        },
        totalCalories() {
            this.total = this.foodCategories.reduce((total, item) => {
                return (
                    total +
                    item.foods.reduce((subtotal, foods) => {
                        return subtotal + foods.weight * foods.caloriesPerGram
                    }, 0)
                )
            }, 0)
        }

    },
}
</script>