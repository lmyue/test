<template>
  <div>
    <div style="margin: 20px 0;">
      业务需求：<br>
      当改变的值与原有的值不同时，显示在意见框内；<br>
      例如：张三默认为批准，当改变张三状态为不批准时，显示：不批准张三；当张三再改为批准时，删除这个意见；
    </div>

    <el-table
      :data="tableData"
      style="width: 100%">
      <el-table-column
        prop="name"
        label="姓名"
        width="180">
      </el-table-column>
      <el-table-column
        label="批复">
        <template slot-scope="scope">
          <el-select v-model="scope.row.replyResult"
                     @change="changeCountryStatus($event,scope.row,scope.$index)">
            <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value">
            </el-option>
          </el-select>
        </template>
      </el-table-column>
    </el-table>

    <div style="font-size: 20px;margin: 6px;">
      意见：
    </div>
    <el-input type="text" v-model="content"/>
  </div>
</template>

<script>
  export default {
    name: 'demo',
    data() {
      return {
        content:'',
        tableData:[
          {
            name:'张三',
            replyResult:'批准',
          }, {
            name:'李四',
            replyResult:'不批准',
          }, {
            name:'王五',
            replyResult:'取消',
          },{
            name:'赵六',
            replyResult:'批准',
          },
        ],
        options: [{
          value: '批准',
          label: '批准'
        }, {
          value: '不批准',
          label: '不批准'
        }, {
          value: '取消',
          label: '取消'
        }],
        value: '',
        //历史批准状态
        tableReplyResultList:[],
        //改变批准状态自动生成审批意见
        contentReplyResultList:{
          agree:[],
          disAgree:[],
          cancle:[],
        },
        //同意
        agreeContent:'',
        //不同意
        disAgreeContent:'',
        //取消
        cancleContent:''
      }
    },
    mounted(){
      this.tableData.forEach(item => {
        this.tableReplyResultList.push(item.replyResult);
      });

    },
    methods:{
      changeCountryStatus(e,row,index){
        //初始化
        this.$set(this.contentReplyResultList.agree,index,row.null)
        this.$set(this.contentReplyResultList.disAgree,index,null)
        this.$set(this.contentReplyResultList.cancle,index,null)
        //判断并赋值
        if(this.tableReplyResultList[index] !== row.replyResult){
          if(e === '批准'){
            this.$set(this.contentReplyResultList.agree,index,row.name)
          }else if(e === '不批准'){
            this.$set(this.contentReplyResultList.disAgree,index,row.name)
          }else if(e === '取消'){
            this.$set(this.contentReplyResultList.cancle,index,row.name)
          }
        }

        // 转为意见
        //1、如果存在不为null的值，则批准
        let agree = this.contentReplyResultList.agree.filter(function(val){
          return !(!val || val === "");
        });
        if(agree.length > 0){
          this.agreeContent = '批准' + agree.join('、')+'；';
        }else{
          this.agreeContent = ''
        }

        //2、如果存在不为null的值，则不批准
        let disagree = this.contentReplyResultList.disAgree.filter(function(val){
          return !(!val || val === "");
        });
        if(disagree.length > 0){
          this.disAgreeContent = '不批准' + disagree.join('、')+'；'
        }else{
          this.disAgreeContent = ''
        }

        //3、如果存在不为null的值，则取消
        let cancle = this.contentReplyResultList.cancle.filter(function(val){
          return !(!val || val === "");
        });
        if(cancle.length > 0){
          this.cancleContent = '取消' + cancle.join('、')+'；'
        }else{
          this.cancleContent = '';
        }

        this.content = this.agreeContent + this.disAgreeContent + this.cancleContent
      }
    }
  }
</script>

<style scoped>

</style>
