<template>
  <div class="target-container">
    <Row class="target-row-up">
      <iCol span="24">
        <div>
          <Card class="target-card-up">
            <img src="" alt="">
            <RadioGroup class="radio-group" type="button">
              <Radio label="1">增肌</Radio>
              <Radio label="2">减脂</Radio>
            </RadioGroup>
          </Card>
        </div>
      </iCol>
    </Row>
    <Row class="target-row-down">
      <iCol span="24">
        <div class="target-card">
          <Card class="target-card-down">
            <RadioGroup class="radio-group" type="button">
              <Radio label="1">轻度</Radio>
              <Radio label="2">中度</Radio>
              <Radio label="3">重度</Radio>
            </RadioGroup>
            <Divider/>
            <Button type="primary" @click="insertTarget">创建健身计划</Button>
          </Card>
        </div>
      </iCol>
    </Row>
  </div>
</template>
<script>
  export default {
    data() {
      return {
        targetType: 1,
        degree: 1
      }
    },
    methods: {
      insertTarget() {
        this.axios.post('user/insertGoal', {
            goal_type: this.targetType,
            goal: this.degree
          })
          .then(res => {
            if (res.data.code == 200) {
              this.$Message.info("创建成功");
              this.$store.dispatch('plan');
              this.$router.push('/Plan');
            } else {
              this.$Message.info("创建失败");
            }
          })
          .catch(err => console.log(err));
      }
    }
  }

</script>
<style>
  .target-container {
    height: 100vh;
    padding: 0px 400px;
  }

  .target-row-up {
    padding-top: 84px;
  }

  .radio-group {}

</style>
