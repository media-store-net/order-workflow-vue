<template>
    <ion-page>
        <ion-header>
            <ion-toolbar color="primary">
                <ion-title>Order Workflow</ion-title>
            </ion-toolbar>
        </ion-header>
        <ion-content>
            <ion-list>
                <ion-list-header>
                    <ion-label>Orders Pool</ion-label>
                </ion-list-header>
                <ion-item v-for="order in orderList" :key="order.id" @click="$router.push({name: 'OrderDetails'})">
                    <ion-note slot="start">{{order.status}}</ion-note>
                    <span>{{order.car}}</span> <span>-</span> <span><i>({{order.regNumber}})</i></span>
                    <ion-note slot="end">{{order.date}}</ion-note>
                </ion-item>
            </ion-list>
        </ion-content>
        <ion-fab vertical="bottom" horizontal="end" slot="fixed">
            <ion-fab-button @click="$router.push({ name: 'Settings' })">
                <ion-icon name="ellipsis-vertical-outline"></ion-icon>
            </ion-fab-button>
        </ion-fab>
    </ion-page>
</template>

<script>
	import {ellipsisVerticalOutline} from "ionicons/icons";
	import {addIcons} from "ionicons";
	import axios from "axios";

	addIcons({
		"ios-ellipsis-vertical-outline": ellipsisVerticalOutline,
		"md-ellipsis-vertical-outline": ellipsisVerticalOutline
	});

	export default {
		name: "Home",
		data() {
			return {
				orderList: null,
				selectedOrder: {}
			}
		},
		mounted() {
			if (!this.orderList) {
				axios.get("../orderSchema.json").then((res) => {
					console.log(res.data)
					this.orderList = res.data;
				});
			}
		}
	}
</script>

<style scoped>
    ion-list-header {
        justify-content: center;
        align-items: center;
    }

</style>
