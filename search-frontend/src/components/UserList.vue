<template>
        <a-list item-layout="horizontal" :data-source="props.userList">
        <template #renderItem="{ item }">
            <a-list-item>
                <a-card hoverable style="width: 140px">
                    <template #cover>
                        <img alt="example" src="https://os.alipayobjects.com/rmsportal/QBnOOoLaAfKPirc.png"
                             style="height: 120px;width:120px;margin-top: 10px;margin-left: 10px"/>
                    </template>
                    <a-card-meta :title="item.userName">
                        <template #description>{{item.userProfile}}</template>
                    </a-card-meta>
                </a-card>
            </a-list-item>
        </template>
    </a-list>
</template>

<script setup lang="ts">
import {withDefaults,defineProps} from "vue";
interface Props {
    userList:any[];
}
const props=withDefaults(defineProps<Props>(),{
    userList:()=>[],
});

</script>

<style scoped></style>