<template>
  <div class="hello">
    <section class="hero">
      <div class="hero-body">
        <div class="container has-text-centered">
          <h1 class="title">
            {{title}}
          </h1>
          <h2 class="subtitle">
            {{day}}
          </h2>
        </div>
      </div>
    </section>
    <div class="container">
      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">姓名</label>
        </div>
        <div class="field-body">
          <div class="field">
            <p class="control is-expanded has-icons-left">
              <input v-model="name" class="input" type="text" placeholder="请输入真实姓名"> <span
                class="icon is-small is-left"> <i class="fas fa-user"></i>
              </span>
            </p>
          </div>
        </div>
      </div>

      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">手机</label>
        </div>
        <div class="field-body">
          <div class="field">
            <p class="control is-expanded has-icons-left">
              <input v-model="phone" class="input" type="text" placeholder="请输入手机号"> <span
                class="icon is-small is-left"> <i class="fas fa-phone"></i>
              </span>
            </p>
          </div>
        </div>
      </div>

      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">部门</label>
        </div>
        <div class="field-body">
          <div class="field is-narrow">
            <div class="control">
              <div class="select is-fullwidth">
                  <select v-model="depart">
                    <option disabled value="">请选择部门</option>
                    <option>Office</option>
                    <option>HR</option>
                    <option>RD</option>
                  </select>

              </div>
            </div>
          </div>
        </div>
      </div>

      <div class="field is-horizontal">
        <div class="field-label">
          <label class="label">外观</label>
        </div>
        <div class="field-body">
          <div class="field is-narrow">
            <div class="control">
              <label class="radio"> <input type="radio" value="a" v-model="appearance">
                满意
              </label> <label class="radio"> <input type="radio" value="b" v-model="appearance">
                一般
              </label><label class="radio"> <input type="radio" value="c" v-model="appearance">
                不满意
              </label>
            </div>
          </div>
        </div>
      </div>
      
      <div class="field is-horizontal">
        <div class="field-label">
          <label class="label">性能</label>
        </div>
        <div class="field-body">
          <div class="field is-narrow">
            <div class="control">
              <label class="radio"> <input type="radio" value="a" v-model="performance">
                满意
              </label> <label class="radio"> <input type="radio" value="b" v-model="performance">
                一般
              </label><label class="radio"> <input type="radio" value="c" v-model="performance">
                不满意
              </label>
            </div>
          </div>
        </div>
      </div>

      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">改进方向</label>
        </div>
        <div class="field-body">
          <div class="field">
            <div class="control">
              <label class="checkbox"> <input
                  type="checkbox"
                  v-model="changes.appearance"
                  true-value="yes"
                  false-value="no"
                > 外观
              </label> <label class="checkbox"> <input
                  type="checkbox"
                  v-model="changes.performance"
                  true-value="yes"
                  false-value="no"
                > 性能
              </label> <label class="checkbox"> <input
                  type="checkbox"
                  v-model="changes.photograph"
                  true-value="yes"
                  false-value="no"
                > 拍照
              </label> <label class="checkbox"> <input
                  type="checkbox"
                  v-model="changes.thickness"
                  true-value="yes"
                  false-value="no"
                > 厚度
              </label>
            </div>
          </div>
        </div>
      </div>
      <div class="field is-horizontal">
        <div class="field-label is-normal">
          <label class="label">意见</label>
        </div>
        <div class="field-body">
          <div class="field">
            <div class="control">
              <textarea v-model="idea" class="textarea"
                placeholder="请将您的其他意见写在这里"></textarea>
            </div>
          </div>
        </div>
      </div>

      <div class="field is-horizontal">
        <div class="field-label">
          <!-- Left empty for spacing -->
        </div>
        <div class="field-body">
          <div class="field">
            <div class="control">
              <button @click="submitForm()" class="button is-primary">提交</button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <footer class="footer">
      <div class="content has-text-centered">
        <p>
          <strong>Bulma</strong> by <a href="https://jgthms.com">Jeremy Thomas</a>. The source code is licensed
          <a href="http://opensource.org/licenses/mit-license.php">MIT</a>. The website content
          is licensed <a href="http://creativecommons.org/licenses/by-nc-sa/4.0/">CC BY NC SA 4.0</a>.
        </p>
      </div>
    </footer>
  </div>
</template>

<script>
require ('./../assets/axios.min.js')
require ('./../assets/fontawesome')
require ('./../assets/bulma.min.css')
export default {
  name: 'HelloWorld',
  data () {
    return {
      title:"手机满意度调查",
      day: Date(),
      name: '',
      phone: '',
      depart: '',
      appearance:'',
      performance:'',
      changes:{appearance:'no', performance:'no', photograph:'no', thickness:'no'},
      idea: ''
    }
  },
  mounted(){

  },
  methods:{
    submitForm(){
          let that = this
          const formData = {
              name: that.name,
              phone: that.phone,
              depart: that.depart,
              appearance:that.appearance,
              performance:that.performance,
              changes: that.changes,
              idea: that.idea

          }
          console.log(formData)
          axios.post('https://veg.kim/api/v1/forms', formData).then(response => {
              console.log(`response.data`)
          })
      }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
