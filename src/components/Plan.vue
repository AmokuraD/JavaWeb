<template>
<div class="plan-container">
  <Form class="Plan">
    <FormItem label="运动计划">
      <Input v-model="plan_content" readonly />
    </FormItem>
    <FormItem label="食物计划" v-for="foodlist in plan_food" :key=foodlist.index>
      <Input v-for="food in foodlist" :key="food.food_name" readonly v-model="food.food_name"/>
    </FormItem>
  </Form>
</div>
  
</template>
<script>
  export default {
    data() {
      return {
        plan_content: null,
        plan_food: []
      }
    },
    methods: {
      plan() {
        this.axios.post('/plan/findPlan')
          .then(res => {
            console.log(res);
            this.plan_content = res.data.data.gymPlan.plan_content;
            this.plan_food = res.data.data.list;
          })
          .catch(err => console.log(err));
      }
    },
    mounted() {
      this.plan();
    }
  }

</script>
<style>
  .plan-container{
    padding: 84px 200px;
    height: 100vh;
  }

</style>
