<template>
    <el-card class="box-card" shadow="always">
        <div class="text item">
            <b>{{data.name}}</b><br/>
            {{data.author}}<br/>
            {{data.year}}, {{data.pages}} стр.
        </div>
    </el-card>
</template>

<script>
export default {
  name: "Card",
  props: ["data"]
};
</script>

<style>
.text {
  font-size: 14px;
  text-align: center;
}

.item {
  padding: 5px 0;
}

.box-card {
  margin: 5px;
}
</style>