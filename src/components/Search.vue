<template>
    <div>
        <el-row :gutter="10" type="flex" justify="center">
            <el-col :xl="2" :lg="8" :md="10" :sm="16" >
                <el-input placeholder="Искать в библиотеке" class="search-field" size="small"
                    v-model="query" clearable
                    @clear="clear" @keyup.enter.native="search"></el-input>
            </el-col>
        </el-row>
        <el-row v-if="rows && rows.length">
            <el-col :span="8" v-for="(row) in rows" :key="row.id">
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
.search-field {
    margin-bottom: 20px;
}
</style>