<template>
    <div>
        <el-row :gutter="20" >
            <el-col :span="8" >
                <el-card style="margin-bottom: 20px">
                        <div class="el-page-header__title" style="width: 100%; height: 200%; text-align: center; margin-bottom: 20px">
                            <h2>角色基础信息<br/></h2>
                        </div>
                        <div class="form-box" >
                            <el-form ref="form" :model="form" label-width="80px" style="width: 70%;">
                                         <el-form-item label="姓名" >
                                            <el-input v-model="form.name"  style="width: 100%;"></el-input>
                                        </el-form-item>
                                <el-row style="margin-bottom: 0px">
                                    <el-col span="12">
                                        <el-form-item label="性别">
                                            <el-input v-model="form.sex"  style="width: 100%; "></el-input>
                                        </el-form-item>
                                    </el-col>
                                    <el-col span="12">
                                            <el-form-item label="种族">
                                                <el-input v-model="form.race"  style="width: 100%;"></el-input>
                                            </el-form-item>
                                    </el-col>
                                </el-row>
                                <el-row style="margin-bottom: 0px">
                                    <el-col span="12">
                                        <el-form-item label="身高">
                                            <el-input v-model="form.height"  style="width: 100%;"></el-input>
                                        </el-form-item>
                                        </el-col>
                                     <el-col span="12">
                                        <el-form-item label="体重">
                                            <el-input v-model="form.weight"  style="width:100%;"></el-input>
                                        </el-form-item>
                                    </el-col>
                                </el-row>
                                <el-row style="margin-bottom: 0px">

                                    <el-col span="12">
                                        <el-form-item label="信仰">
                                            <el-input v-model="form.belief"  style="width: 100%;"></el-input>
                                         </el-form-item>
                                    </el-col>
                                    <el-col span="12">
                                         <el-form-item label="年龄">
                                            <el-input v-model="form.age"  style="width: 100%;"></el-input>
                                        </el-form-item>
                                    </el-col>
                                </el-row>
                                <el-row style="margin-bottom: 0px">
                                    <el-col span="12">
                                        <el-form-item label="信仰心">
                                    <el-input v-model="form.faith"  style="width:100%;"></el-input>
                                </el-form-item>
                                    </el-col>
                                      <el-col span="12">
                                          <el-form-item label="惯用手">
                                    <el-input v-model="form.hand"  style="width: 100%;"></el-input>
                                </el-form-item>
                                      </el-col>
                                </el-row>


                                <el-form-item label="性格">
                                    <el-input v-model="form.personality" style="width: 100%;"></el-input>
                                </el-form-item>
                                <el-form-item label="种族特性">
                                    <el-input v-model="form.racespec"  type="textarea" rows="3" style="width: 100%;"></el-input>
                                </el-form-item>
                                <el-form-item label="从属角色">
                                    <el-input v-model="form.role"  style="width: 100%;"></el-input>
                                </el-form-item>
                                <el-form-item>
                                    <el-button type="primary" @click="onSubmit">保存</el-button>
                                    <el-button>取消</el-button>
                                </el-form-item>
                            </el-form>
                        </div>
                </el-card>
                <el-card>
                <div class="el-page-header__title" style="width: 100%; height: 200%; text-align: center; margin-bottom: 20px">
                            <h2>角色简介<br/></h2>
                        </div>
                        <div class="form-box" >
                            <el-form ref="form" :model="form" label-width="80px" style="width: 70%;">
                                <el-form-item label="">
                                    <el-input type="textarea" rows="3" v-model="form.roleintro"></el-input>
                                </el-form-item>
                                 <el-form-item>
                                    <el-button type="primary" @click="onSubmit">保存</el-button>
                                    <el-button>取消</el-button>
                </el-form-item>
                                </el-form>
                        </div>
                </el-card>
            </el-col>
            <el-col :span="16">


                <el-card shadow="hover" style="height:825px;">
                    <div class="el-page-header__title" style="width: 100%; height: 200%; text-align: center; margin-bottom: 20px">
                            <h2>角色技能<br/></h2>
                        </div>
                   <el-table
                :data="tableData"
                border
                class="table"
                ref="multipleTable"
                header-cell-class-name="table-header"
                @selection-change="handleSelectionChange"
            >
                <el-table-column prop="skillname" label="技能名" align="center"></el-table-column>
                <el-table-column prop="level" label="等级" align="center"></el-table-column>
                <el-table-column prop="current-exp" label="目前经验" align="center"></el-table-column>
                <el-table-column prop="exp-to-next-level" label="升级所需经验" align="center"></el-table-column>
<!--                <el-table-column label="操作" width="180" align="center">-->
<!--                    <template slot-scope="scope">-->
<!--                        <el-button-->
<!--                            type="text"-->
<!--                            icon="el-icon-edit"-->
<!--                            @click="handleEdit(scope.$index, scope.row)"-->
<!--                        >编辑</el-button>-->
<!--                        <el-button-->
<!--                            type="text"-->
<!--                            icon="el-icon-delete"-->
<!--                            class="red"-->
<!--                            @click="handleDelete(scope.$index, scope.row)"-->
<!--                        >删除</el-button>-->
<!--                    </template>-->
<!--                </el-table-column>-->
            </el-table>
                </el-card>
            </el-col>
        </el-row>

    </div>
</template>

<script>
import Schart from 'vue-schart';
import bus from '../common/bus';
export default {
    name: 'dashboard',
    data() {
        return {
            name: localStorage.getItem('ms_username'),
            form: {
                name: '水野权藏',
                sex: '男',
                race: '鲸天狗',
                height: 184,
                weight: 78,
                belief: '大神教',
                age: 18,
                faith: '中等',
                hand: '右',
                personality: '较易冲动、自信、直率',
                racespec: '允许在水下活动无惩罚，拥有特殊的种族专属“赐福系”魔法',
                role: 'xxx',
                roleintro: '出生于天狗国外圈的平凡家族的鲸天狗，成年之后子承父业，接下了他爹御海行者的职位，守护着天狗国领海的安全。',
            },
            tableData:[{
                        "skillname": "防御",
                        "level": 0,
                        "current-exp": 0,
                        "exp-to-next-level": 6,
                    },
                    {
                        "skillname": "搬运",
                        "level": 0,
                        "current-exp": 0,
                        "exp-to-next-level": 6,
                    },
                    {
                        "skillname": "恐吓",
                        "level": 0,
                        "current-exp": 0,
                        "exp-to-next-level": 6,
                    },
                    {
                        "skillname": "讲价",
                        "level": 0,
                        "current-exp": 0,
                        "exp-to-next-level": 6,
                    },
                ],
            "pageTotal": 6
        };
    },
    components: {
        Schart
    },
    computed: {
        role() {
            return this.name === 'admin' ? '超级管理员' : '普通用户';
        }
    },
    // created() {
    //     this.handleListener();
    //     this.changeDate();
    // },
    // activated() {
    //     this.handleListener();
    // },
    // deactivated() {
    //     window.removeEventListener('resize', this.renderChart);
    //     bus.$off('collapse', this.handleBus);
    // },
    methods: {
        changeDate() {
            const now = new Date().getTime();
            this.data.forEach((item, index) => {
                const date = new Date(now - (6 - index) * 86400000);
                item.name = `${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()}`;
            });
        },
        // handleListener() {
        //     bus.$on('collapse', this.handleBus);
        //     // 调用renderChart方法对图表进行重新渲染
        //     window.addEventListener('resize', this.renderChart);
        // },
        // handleBus(msg) {
        //     setTimeout(() => {
        //         this.renderChart();
        //     }, 200);
        // },
        // renderChart() {
        //     this.$refs.bar.renderChart();
        //     this.$refs.line.renderChart();
        // }
        onSubmit() {
            this.$message.success('提交成功！');
        }
    }
};
</script>

<style scoped>
.el-row {
    margin-bottom: 20px;
}

.grid-content {
    display: flex;
    align-items: center;
    height: 100px;
}

.grid-cont-right {
    flex: 1;
    text-align: center;
    font-size: 14px;
    color: #999;
}

.grid-num {
    font-size: 30px;
    font-weight: bold;
}

.grid-con-icon {
    font-size: 50px;
    width: 100px;
    height: 100px;
    text-align: center;
    line-height: 100px;
    color: #fff;
}

.grid-con-1 .grid-con-icon {
    background: rgb(45, 140, 240);
}

.grid-con-1 .grid-num {
    color: rgb(45, 140, 240);
}

.grid-con-2 .grid-con-icon {
    background: rgb(100, 213, 114);
}

.grid-con-2 .grid-num {
    color: rgb(45, 140, 240);
}

.grid-con-3 .grid-con-icon {
    background: rgb(242, 94, 67);
}

.grid-con-3 .grid-num {
    color: rgb(242, 94, 67);
}

.user-info {
    display: flex;
    align-items: center;
    padding-bottom: 20px;
    border-bottom: 2px solid #ccc;
    margin-bottom: 20px;
}

.user-avator {
    width: 120px;
    height: 120px;
    border-radius: 50%;
}

.user-info-cont {
    padding-left: 50px;
    flex: 1;
    font-size: 14px;
    color: #999;
}

.user-info-cont div:first-child {
    font-size: 30px;
    color: #222;
}

.user-info-list {
    font-size: 14px;
    color: #999;
    line-height: 25px;
}

.user-info-list span {
    margin-left: 70px;
}

.mgb20 {
    margin-bottom: 20px;
}

.todo-item {
    font-size: 14px;
}

.todo-item-del {
    text-decoration: line-through;
    color: #999;
}

.schart {
    width: 100%;
    height: 300px;
}
</style>
