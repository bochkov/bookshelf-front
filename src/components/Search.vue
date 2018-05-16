<template>
    <div>
        <el-row :gutter="10" type="flex" justify="center">
            <el-col :xl="6" :lg="6" :md="6" :sm="8" >
                <el-input placeholder="Искать в библиотеке" 
                    @keyup.enter.native="search" v-model="query" clearable></el-input>
            </el-col>
            <el-col :span="2">
                <el-button icon="el-icon-search" @click="search" circle></el-button>
            </el-col>
        </el-row>
        <el-row v-if="rows && rows.length">
            <el-col v-for="(row) in rows" :key="row.id">
                <Card :data=row></Card>
            </el-col>
        </el-row>
    </div>
</template>

<script>
    import axios from 'axios'
    import Card from './Card'

    export default {
        name: 'Search',
        components: {Card},
        data() {
            return {
                query: "",
                rows: []
            }
        },
        methods: {
            search: function () {
                if (this.query === '')
                    this.msg('Введите что-нибудь', 'warning');
                else
                    axios.post('/api/search', this.query, {headers: {'Content-Type':'text/plain'}})
                        .then(data => {
                            this.clear();
                            if (data.data.length === 0)
                                this.msg('Ничего не найдено', 'warning');
                            else
                                this.rows.push(...data.data);
                        })
                        .catch(() => {
                            this.msg('Невозможно выполнить запрос', 'error');
                        });
            },
            clear: function () {
                this.rows.splice(0, this.rows.length);
            },
            msg: function(text, type) {
                this.$message({
                    message: text,
                    type: type,
                    center: true,
                })
            },
        }
    }
</script>

<style>

</style>