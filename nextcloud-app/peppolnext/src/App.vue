<template>
	<div id="content">
		<AppNavigation>
			<AppNavigationNew text="Create New Invoice" icon="icon-add" @new-item="function(value){alert(value)}" />
			<template #list>
				<AppNavigationItem title="Messages" :allow-collapse="true" :open="true">
					<template>
						<AppNavigationItem icon="icon-download" title="Inbox" to="/message/list/Inbox" />
						<AppNavigationItem icon="icon-upload" title="Outbox" to="/message/list/Outbox" />
						<AppNavigationItem icon="icon-group" title="Customers" to="/message/list/Customers" />
						<AppNavigationItem icon="icon-public" title="Suppliers" to="/message/list/Suppliers" />
						<AppNavigationItem icon="icon-add" title="Compose" to="/message/new" />
						<AppNavigationItem icon="icon-delete" title="Trash" to="/message/list/Trash" />
					</template>
				</AppNavigationItem>

				<AppNavigationItem title="Network" :allow-collapse="true" :open="true">
					<template>
						<AppNavigationItem title="Received Invoices" to="/connection/list">
							<template #counter>
								<CounterBubble v-if="notification.messages > 0" type="outlined">{{notification.messages}}</CounterBubble>
							</template>
						</AppNavigationItem>
						<AppNavigationItem title="Connection Requests" to="/connection/list">
							<template #counter>
								<CounterBubble v-if="notification.connection_requests > 0" type="outlined">{{notification.connection_requests}}</CounterBubble>
							</template>
						</AppNavigationItem>
						<AppNavigationItem title="Sent Requests" to="/connection/list" />
						<AppNavigationItem title="My Network" to="/connection/list" />
						<AppNavigationItem title="Add Contact" to="/connection/new" />
					</template>
				</AppNavigationItem>
			</template>
			<template #footer>
				<AppNavigationSettings>
					<div class="row">
						<div class="col-5">
							<input type="text" placeholder="Fullname" v-model="setting.fullname" />
						</div>
						<div class="col-5">
							<input type="email" placeholder="Email" v-model="setting.email" />
						</div>
					</div>
					<div class="row">
						<div class="col-5">
							<input type="text" placeholder="Peppol scheme" v-model="setting.peppolScheme" />
						</div>
						<div class="col-5">
							<input type="text" placeholder="Peppol Id" v-model="setting.peppolId" />
						</div>
					</div>
					<div class="row">
						<div class="col-5">
							<input type="tel" placeholder="Phone no" v-model="setting.phoneNo" />
						</div>
						<div class="col-5">
							<input type="tel" placeholder="Fax no" v-model="setting.faxNo" />
						</div>
					</div>
					<div>
						<p>Address:</p>
						<div class="row">
							<div class="col-5">
								<input placeholder="Country (ISO)" v-model="setting.country" />
							</div>
							<div class="col-5">
								<input placeholder="City" v-model="setting.city" />
							</div>
						</div>
						<div class="row">
							<div class="col-10">
								<input placeholder="Street address" v-model="setting.street" />
							</div>
						</div>
						<div class="row">
							<div class="col-10">
								<input placeholder="Extended street address" v-model="setting.additionStreet" />
							</div>
						</div>
					</div>
					<div class="row">
						<div class="col-6">
							<input placeholder="Postal zone" v-model="setting.postalZone" />
						</div>
						<div class="col-4">
							<input placeholder="Building no" v-model="setting.buildingNo" />
						</div>
					</div>
					<div class="row">
						<button id="submit" @click="updateSettings">Submit</button>
					</div>

				</AppNavigationSettings>
			</template>
		</AppNavigation>
		<AppContent>
			<router-view></router-view>
		</AppContent>
	</div>
</template>

<script>
import AppNavigation from '@nextcloud/vue/dist/Components/AppNavigation'
import AppNavigationItem from '@nextcloud/vue/dist/Components/AppNavigationItem'
import AppNavigationNew from '@nextcloud/vue/dist/Components/AppNavigationNew'
import AppContent from '@nextcloud/vue/dist/Components/AppContent'
import AppNavigationSettings from '@nextcloud/vue/dist/Components/AppNavigationSettings'
import axios from '@nextcloud/axios'
import CounterBubble from '@nextcloud/vue/dist/Components/CounterBubble'

export default {
	name: 'App',
	components: {
		AppNavigation,
		AppNavigationItem,
		AppNavigationNew,
		AppContent,
		AppNavigationSettings,
		CounterBubble,
	},
	mounted: function() {
		this.loadAllSettings(this)
		this.getNotifications(this)
	},
	data: () => {
		return {
			setting: {},
			notification: {
				messages: 0,
				connection_requests: 0
			}
		}
	},
	methods: {
		loadAllSettings(vm) {
			axios.get('/index.php/apps/peppolnext/api/v1/setting')
				.then(function(response) {
					vm.setting = response.data
				})
				.catch(function(error) {})
		},
		updateSettings(vm) {
			const payload = { body: this.setting }
			axios.post('/index.php/apps/peppolnext/api/v1/setting', payload)
				.then(function(response) {}).catch(function(error) {})
		},
		getNotifications(vm) {
			axios.get('/index.php/apps/peppolnext/api/v1/message/notifications')
				.then(function(response) {
					vm.notification.messages = response.data.messages
					vm.notification.connection_requests = response.data.connection_requests
				})
				.catch(function(error) {})
		}
	}
}
</script>
<style scoped>
	p{
		font-weight: bolder;
	}
</style>
