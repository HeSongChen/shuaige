<template>
    <div class="pos">
        <div>
            <el-row>
                <el-col :span='7' id="list">
                    <el-tabs>
                        <el-tab-pane label='点餐'>
                            <el-table :data='tableData' border show-summary style="width:100%">
                                <el-table-column label='商品' prop='name'></el-table-column>
                                <el-table-column label='数量' prop='count'></el-table-column>
                                <el-table-column label='金额' prop='pri'></el-table-column>
                                <el-table-column label='操作' width='150'>
                                    <template  slot-scope="scope">
                                          <el-button  type="primary" size='mini'>删除</el-button>
                                          <el-button  type="primary" size='mini'>添加</el-button>
                                    </template>
                                </el-table-column>
                            </el-table>
                        </el-tab-pane>  
                        <el-tab-pane label='外卖'>
                            <el-table :data='tableData2' border show-summary style="width:100%">
                                <el-table-column label='商品' prop='name'></el-table-column>
                                <el-table-column label='数量' prop='count'></el-table-column>
                                <el-table-column label='金额' prop='pri'></el-table-column>
                                <el-table-column label='操作'  width='150'>
                                    <template  slot-scope="scope">
                                          <el-button  type="primary" size='mini'>删除</el-button>
                                          <el-button  type="primary" size='mini'>添加</el-button>
                                    </template>
                                </el-table-column>
                            </el-table>
                        </el-tab-pane>
                    </el-tabs>
                <el-row>
                    <el-button type="warning">清空</el-button>
                    <el-button type="danger">购买</el-button>
                </el-row> 
                </el-col>
                <el-col :span='15'>
                    <div class="pro">
                        <div class="title">吃货的地方</div>
                        <div class="pro-list">
                            <ul>
                               <li v-for='lly in pros'>
                                   <span>{{lly.name}}</span>
                                   <span class="pro-pri">￥{{lly.pri}}</span>
                               </li>
                            </ul>
                        </div>
                    </div>
                    <div class="pro-type">
                        <el-tabs>
                            <el-tab-pane label='肥宅区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType1'>
                                        <span class="foodImg"><img :src="val.img" alt=""></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label='儿童区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType2'>
                                        <span class="foodImg"><img :src="val.img" alt=""></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                            <el-tab-pane label='快乐区'>
                                <ul class="ckList">
                                    <li v-for='val in goodType3'>
                                        <span class="foodImg"><img :src="val.img" alt=""></span>
                                        <span class="foodName">{{val.name}}</span>
                                        <span class="foodPri">￥{{val.pri}}</span>
                                    </li>
                                </ul>
                            </el-tab-pane>
                        </el-tabs>
                    </div>
                </el-col>
            </el-row>
        </div>
    </div>
</template>
<script>
import axios from 'axios'
export default {
  name: "Pos",
  data(){
      return {
        tableData:'',
        tableData2:'',
        pros:'',
        goodType1:'',
        goodType2:'',
        goodType3:''
      }
  },
  mounted(){
        let h = document.body.clientHeight;
        let list = document.querySelector('#list');
        list.style.height = h + 'px';
    },
    created(){
      axios.get('http://localhost:8080/static/data.json')
        .then(res => {
            this.tableData = res.data.tableData;
            this.tableData2 = res.data.tableData2;
            this.pros = res.data.pros;
            this.goodType1 = res.data.goodType1;
            this.goodType2 = res.data.goodType2;
            this.goodType3 = res.data.goodType3;
        })
        .catch(err => {
            console.log('网络出错，无法访问')
        })
  }
}
</script>
<style scoped>
  .pro{
    width: 100%;
  }
  .title{
    width: 100%;
    text-align: center;
    height: 50px;
    line-height: 50px;
    background: #77ccdd;
    color: #fff;
    font-size: 18px;
    font-weight: 700;
  }
  .pro-list li{
    list-style: none;
    padding: 10px;
    margin-left: 20px; 
    float: left;
    border:1px solid #77ccdd;
    cursor: pointer;
  }
  .pro-pri{
    color: #77ccdd;
    font-weight: 700;
  }
  .pro-type{
    display: block;
    clear: both;
  }
  .ckList{
    list-style: none;
  }
  /* .btns{
    width: 40%;
    height: 30px;
    font-size: 12px;
    padding: 0;
  } */
  .ckList>li{
    float: left;
    width: 25%;
    height: 200px;
    margin-left: 20px;
    position: relative;
    margin-top: 12px;
  }
  .ckList img{
    width: 100%;
    height: 100%;
    display: block;
  }
  .foodName{
    position: absolute;
    z-index: 10;
    top: 3px;
    left: 50%;
    transform: translateX(-50%);
    font-size: 16px;
    font-weight: 700;
  }
  .foodPri{
    position: absolute;
    z-index: 10;
    top: 0;
    color:#333;
    font-size: 18px;
    font-weight: 900;
    top: 0;
    left: 20%;
  }
</style>