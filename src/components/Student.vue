<template>
    <tr>
        <td v-show="!is_edit">{{ student.studentId }}</td>
        <td v-show="!is_edit">{{ student.name }}</td>
        <td v-show="!is_edit">{{ student.gender }}</td>
        <td v-show="!is_edit">{{ student.phoneNumber }}</td>
        <td v-show="!is_edit">{{ student.email }}</td>
        <td v-show="!is_edit">{{ student.address }}</td>
        <td v-show="!is_edit">{{ student.className }}</td>
        <td v-show="!is_edit">{{ student.grade }}</td>
        <td v-show="!is_edit">{{ student.major }}</td>
        <td v-show="!is_edit">{{ student.counselor }}</td>
        <td v-show="!is_edit">
            <div class="d-flex align-items-center">
                <el-button type="primary" @click="modify">修改</el-button>
                <div style="width: 10px;"></div>
                <el-button type="danger" @click="deleteStudent">删除</el-button>
            </div>
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.studentId">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.name">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.gender">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.phoneNumber">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.email">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.address">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.className">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.grade">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.major">
        </td>
        <td v-show="is_edit">
            <input type="text" class="form-control" v-model="student.counselor">
        </td>
        <td v-show="is_edit">
            <div class="d-flex align-items-center">
                <el-button type="primary" @click="save">保存</el-button>
                <div style="width: 10px;"></div>
                <el-button type="danger" @click="deleteStudent">删除</el-button>
            </div>
        </td>
    </tr>
</template>

import axios from 'axios'
<script>
import axios from 'axios'
export default {
    props: ["student"],
    data() {
        return {
            is_edit: false
        }
    },
    methods: {
        modify() {
            this.is_edit = true
        },
        save() {
            axios({
                url: "http://localhost:8082/update",
                method: "POST",
                data: this.student
            })
            this.is_edit = false;
        },
        deleteStudent() {
            axios({
                url: "http://localhost:8082/delete",
                method: "POST",
                data: this.student
            })
        }

    }
}
</script>

<style></style>