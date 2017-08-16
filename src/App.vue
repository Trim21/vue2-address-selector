<template>
  <div id="projectId">

    <div class="row">
      <div class="col-xs-12 col-sm-12 col-md-12 col-lg-12">
        <el-form ref="form" label-width="80px">

          <el-row class='address'>
            <el-col :span='6'>
              <el-form-item>
                <el-select filterable v-model='form.province' placeholder='请输入省'>
                  <el-option v-for='item in provinces' :key='item.value' :value='item.value'>
                  </el-option>
                </el-select>
              </el-form-item>
            </el-col>

            <el-col :span='6'>
              <el-form-item>
                <el-select v-model='form.city' placeholder='请输入市'>
                  <el-option v-for='item in citys' :key='item.value' :value='item.value'>
                  </el-option>
                </el-select>
              </el-form-item>
            </el-col>


            <el-col :span='6'>
              <el-form-item>
                <el-select v-model='form.country' placeholder='请输入区县'>
                  <el-option v-for='item in countrys' :key='item.value' :value='item.value'>
                  </el-option>
                </el-select>
              </el-form-item>
            </el-col>

            <el-col :span='6'>
              <el-form-item>
                <el-input placeholder='请填写详细地址' :number='true' v-model='data.location_street'>
                </el-input>
              </el-form-item>
            </el-col>
          </el-row>

        </el-form>

      </div>
    </div>

  </div>
</template>

<script>
  import addressData from '@/lib/address'

  function formatData (data) {
    let result = []
    if (!data) return result
    if (Array.isArray(data)) {
      for (let key in data) {
        result.push({
          value: data[key]
        })
      }
    } else {
      for (let key in data) {
        result.push({
          value: key
        })
      }
    }
    return result
  }
  export default {
    name: 'index',
    components: {
    },
    computed: {
      citys () {
        return this.form.province ? formatData(addressData[this.form.province]) : []
      },
      countrys () {
        return this.form.province && this.form.city ? formatData(addressData[this.form.province][this.form.city]) : []
      }
    },
    data () {
      return {
        data: {},
        form: {
          province: '',
          city: '',
          country: ''
        },
        msg: 'Welcome to Your Vue.js App',
        provinces: formatData(addressData)
      }
    }
  }
</script>
<!-- Add 'scoped' attribute to limit CSS to this component only -->
<style scoped>

</style>