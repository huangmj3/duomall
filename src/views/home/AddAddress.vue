<!--新增收货地址-->
<template>
  <div>
    <div class="add-container">
      <div class="add-title">
        <h1>添加收货地址</h1>
      </div>
      <div class="add-box">
        <Form :model="formData" label-position="left" :label-width="100" :rules="ruleInline">
          <FormItem label="收件人" prop="name">
            <i-input v-model="formData.name" size="large"></i-input>
          </FormItem>
          <FormItem label="收件地区" prop="address">
            <Distpicker :province="formData.province" :city="formData.city" :area="formData.area"
                        @province="getProvince" @city="getCity" @area="getArea"></Distpicker>
          </FormItem>
          <FormItem label="收件地址" prop="address">
            <i-input v-model="formData.address" size="large"></i-input>
          </FormItem>
          <FormItem label="手机号码" prop="phone">
            <i-input v-model="formData.phone" size="large"></i-input>
          </FormItem>
          <FormItem label="邮政编码" prop="postalcode">
            <i-input v-model="formData.postcode" size="large"></i-input>
          </FormItem>
        </Form>
      </div>
      <div class="add-submit">
        <Button type="primary" @click="addAddressSuccess">添加地址</Button>
      </div>
    </div>
  </div>
</template>

<script>
  import Distpicker from 'v-distpicker';

  export default {
    name: 'AddAddress',
    data() {
      return {
        formData: {
          addressId: '',
          name: '',
          address: '',
          phone: '',
          postcode: '',
          province: '广东省',
          city: '广州市',
          area: '天河区'
        },
        ruleInline: {
          name: [
            {required: true, message: '请输入姓名', trigger: 'blur'}
          ],
          address: [
            {required: true, message: '请输入地址', trigger: 'blur'}
          ],
          postcode: [
            {required: true, message: '请输入邮政编码', trigger: 'blur'}
          ],
          phone: [
            {required: true, message: '手机号不能为空', trigger: 'blur'},
            // { type: 'string', pattern: /^1[3|4|5|7|8][0-9]{9}$/, message: '手机号格式出错', trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      getProvince(data) {
        this.formData.province = data.value;
      },
      getCity(data) {
        this.formData.city = data.value;
      },
      getArea(data) {
        this.formData.area = data.value;
      },
      addAddressSuccess() {
        this.$alert("添加成功")
        let formData = {
          addressId: '12121',
          name: '黄茂杰',
          address: '111',
          phone: '111',
          postcode: '111',
          province: '广东省',
          city: '广州市',
          area: '天河区'
        }
        this.$store.state.address.push(formData)
        console.log("打印一下新地址对象")
        console.log(this.$store.state.address)
        this.formData.name = ''
        this.formData.address = ''
        this.formData.phone = ''
        this.formData.postcode = ''
        this.province = '广州省'
        this.city = '广州市'
        this.area = '天河区'
      }
    },
    components: {
      Distpicker
    }
  };
</script>

<style scoped>
  .add-container {
    margin: 15px auto;
    width: 60%;
    min-width: 600px;
  }

  .add-title {
    margin-bottom: 15px;
    text-align: center;
  }

  .add-submit {
    display: flex;
    justify-content: center;
  }
</style>
