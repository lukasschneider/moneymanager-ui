<script lang="ts">
import {
		DashboardMainNav,
		UserNav,
	} from "./index.js";
</script>

<div class="hidden flex-col md:flex">
	<div class="border-b">
		<div class="flex h-16 items-center px-4">
			<DashboardMainNav currentSite='expense' />
			<div class="ml-auto flex items-center space-x-4">
				<UserNav />
			</div>
		</div>
	</div>
</div>
