<template>
  <div :data-clazz="model.clazz">
    <div class="panelTitle">{{ i18n['process'] }}</div>
    <div class="panelBody">
      <div class="panelRow">
        <div>{{ i18n['process.id'] }}：</div>
        <el-input
          style="width: 90%; font-size: 12px"
          :disabled="readOnly || !!this.$route.query.type"
          placeholder="必填（唯一标识）"
          :value="model.id"
          @input="
            (value) => {
              onChange('id', value)
            }
          "
        />
      </div>
      <DefaultDetail :model="model" :onChange="onChange" :readOnly="readOnly" />
      <!-- <div class="panelRow">
        <div>{{ i18n['process.category'] }}：</div>
        <el-select
          style="width: 90%; font-size: 12px"
          :disabled="readOnly"
          :value="model.category"
          allow-create
          :filterable="true"
          :filter-method="filterCategory"
          @change="(e) => onChange('category', e)"
        >
          <el-option
            v-for="category in categoryCopy"
            :key="category.id"
            :label="category.name"
            :value="category.id"
          />
        </el-select>
      </div> -->

      <div class="panelRow">
        <div>{{ i18n['process.name'] }}：</div>
        <el-input
          style="width: 90%; font-size: 12px"
          :disabled="readOnly"
          placeholder="请输入流程名称"
          :value="model.name"
          @input="
            (value) => {
              onChange('name', value)
            }
          "
        />
      </div>
      <div class="panelRow">
        <div>默认视图文件路径（以view开头）</div>
        <el-input
          style="width: 90%; font-size: 12px"
          :disabled="readOnly"
          placeholder="请输入视图文件路径（以view开头）"
          type="view"
          :value="model.view"
          @input="
            (value) => {
              onChange('view', value)
            }
          "
        />
      </div>
      <div class="panelRow">
        <div>详情说明：</div>
        <el-input
          style="width: 90%; font-size: 12px"
          :disabled="readOnly"
          type="textarea"
          placeholder="请输入详情说明"
          :value="model.description"
          @input="
            (value) => {
              onChange('description', value)
            }
          "
        />
      </div>
    </div>
  </div>
</template>
<script>
  import DefaultDetail from "./DefaultDetail";
  export default {
    inject: ['i18n'],
    components: {
      DefaultDetail
    },
    props: {
      model: {
        type:Object,
        default: ()=>({}),
      },
      categorys: {
        type: Array,
        default: ()=>([]),
      },
      onChange: {
        type: Function,
        default: ()=>{}
      },
      readOnly:{
        type: Boolean,
        default: false,
      }
    },
    data() {
      return {
        categoryCopy: this.categorys,
      }
    },
    methods: {
      filterCategory(input) {
        if (input) {
          this.categoryCopy = this.categorys.filter((item) => {
            if (!!~item.name.indexOf(input) || !!~item.name.toLowerCase().indexOf(input.toLowerCase())) {
              return true
            }
          })
        } else {
          this.categoryCopy = this.categorys;
        }
      }
    }

  }
</script>
