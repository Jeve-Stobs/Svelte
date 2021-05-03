<svelte:head>
	<script src="https://cdn.jsdelivr.net/gh/alpine-collective/alpine-magic-helpers@0.6.x/dist/component.min.js" on:load={initializeRemarkable}></script>
  	<script src="https://cdnjs.cloudflare.com/ajax/libs/alpinejs/2.8.2/alpine.js" on:load={initializeRemarkable}></script>
    	<script src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.6.0/js/bootstrap.min.js" on:load={initializeRemarkable}></script>
          	<script src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.6.0/js/bootstrap.min.js" on:load={initializeRemarkable}></script>
            <script src="https://code.jquery.com/jquery-3.6.0.min.js" on:load={initializeRemarkable}></script>
</svelte:head>
<DockLayout stretchLastChild="true" backgroundColor="#3c495e">
  <label text="left" dock="left" width="40" backgroundColor="#43b883" />
  <label text="top" dock="top" height="40" backgroundColor="#289062" />
  <label text="right" dock="right" width="40" backgroundColor="#43b883" />
  <label text="bottom" dock="bottom" backgroundColor="#1c6b48" />
</DockLayout>

<page>
    <actionBar title="Home" />
    <gridLayout>
        <label class="info" horizontalAlignment="center" verticalAlignment="middle" textWrap="true">
            <formattedString>
                <span class="fas" text="&#xf135;" />
                <span text=" {message}" />
            </formattedString>
        </label>
    </gridLayout>
    <htmlView html="<div x-data="setup()" x-init="$refs.loading.classList.add('hidden');" :class="{ 'dark': isDark }" @resize.window="watchScreen()">
		<div class="flex h-full antialiased text-gray-900 bg-gray-100 dark:bg-dark dark:text-light">
			<!-- Loading screen -->
			<div x-ref="loading" class="fixed inset-0 z-50 flex items-center justify-center text-2xl font-semibold text-white bg-indigo-800">
				Loading.....
			</div>
			<!-- Sidebar -->
			<!-- Backdrop -->
			<div x-show="isSidebarOpen" @click="isSidebarOpen = false" class="fixed inset-0 z-10 bg-indigo-800 lg:hidden" style="opacity: 0.5"
			 aria-hidden="true"></div>
			<aside x-show="isSidebarOpen" x-transition:enter="transition-all transform duration-300 ease-in-out" x-transition:enter-start="-translate-x-full opacity-0"
			 x-transition:enter-end="translate-x-0 opacity-100" x-transition:leave="transition-all transform duration-300 ease-in-out"
			 x-transition:leave-start="translate-x-0 opacity-100" x-transition:leave-end="-translate-x-full opacity-0" x-ref="sidebar"
			 @keydown.escape="window.innerWidth <= 1024 ? isSidebarOpen = false : ''" tabindex="-1" class="fixed inset-y-0 z-10 flex flex-shrink-0 overflow-hidden bg-white border-r lg:static dark:border-indigo-800 dark:bg-darker focus:outline-none">
				<!-- Mini column -->
				<div class="flex flex-col flex-shrink-0 h-full px-2 py-4 border-r dark:border-indigo-800 fixed">
					<!-- Brand -->
					<div class="flex-shrink-0">
						<a href="#" class="inline-block text-xl font-bold tracking-wider text-indigo-700 uppercase dark:text-light">
							MBC
						</a>
					</div>
					<div class="flex flex-col items-center justify-center flex-1 space-y-4">
						<div class="flex flex-col items-center justify-center">
							<!-- User avatar button -->
							<div class="" x-data="{ open: false }">
								<button
										@click="open = !open; $nextTick(() => { if(open){ $refs.userMenu.focus() } })"
										type="button"
										aria-haspopup="true"
										:aria-expanded="open ? 'true' : 'false'"
										class="block transition-opacity duration-200 rounded-full dark:opacity-75 dark:hover:opacity-100 focus:outline-none focus:ring dark:focus:opacity-100"
									>
										<a href="account.html">
											<span class="sr-only">User menu</span>
											<img
												class="w-10 h-10 rounded-full"
												src="https://jeve-stobs.github.io/resources/images/favicon.png"
												alt="Samuel Casey"
											/>
										</a>
									</button>

									<!-- User dropdown menu -->
									<div
										x-show="open"
										x-ref="userMenu"
										x-transition:enter="transition-all transform ease-out"
										x-transition:enter-start="-translate-y-1/2 opacity-0"
										x-transition:enter-end="translate-y-0 opacity-100"
										x-transition:leave="transition-all transform ease-in"
										x-transition:leave-start="translate-y-0 opacity-100"
										x-transition:leave-end="-translate-y-1/2 opacity-0"
										@click.away="open = false"
										@keydown.escape="open = false"
										class="absolute w-56 py-1 mb-4 bg-white rounded-md shadow-lg min-w-max left-5 bottom-full ring-1 ring-black ring-opacity-5 dark:bg-dark focus:outline-none"
										tabindex="-1"
										role="menu"
										aria-orientation="vertical"
										aria-label="User menu"
									>
										<a
											href="#"
											role="menuitem"
											class="block px-4 py-2 text-sm text-gray-700 transition-colors hover:bg-gray-100 dark:text-light dark:hover:bg-indigo-600"
											>Profile
										</a>
										<a
											href="#"
											role="menuitem"
											class="block px-4 py-2 text-sm text-gray-700 transition-colors hover:bg-gray-100 dark:text-light dark:hover:bg-indigo-600"
										>
											Logout
										</a>
									</div>
								</div>
							</div>
							<!-- Notification button -->
							<button
								@click="openNotificationsPanel"
								class="p-2 text-indigo-400 transition-colors duration-200 rounded-full bg-indigo-50 hover:text-indigo-600 hover:bg-indigo-100 dark:hover:text-light dark:hover:bg-indigo-700 dark:bg-dark focus:outline-none focus:bg-indigo-100 dark:focus:bg-indigo-700 focus:ring-indigo-800"
							>
								<span class="sr-only">Open Notification panel</span>
								<svg
									class="w-7 h-7"
									xmlns="http://www.w3.org/2000/svg"
									fill="none"
									viewbox="0 0 448 512"
									stroke="currentColor"
									aria-hidden="true"
								>
									<path
										fill="currentColor"
										d="M439.39 362.29c-19.32-20.76-55.47-51.99-55.47-154.29 0-77.7-54.48-139.9-127.94-155.16V32c0-17.67-14.32-32-31.98-32s-31.98 14.33-31.98 32v20.84C118.56 68.1 64.08 130.3 64.08 208c0 102.3-36.15 133.53-55.47 154.29-6 6.45-8.66 14.16-8.61 21.71.11 16.4 12.98 32 32.1 32h383.8c19.12 0 32-15.6 32.1-32 .05-7.55-2.61-15.27-8.61-21.71zM67.53 368c21.22-27.97 44.42-74.33 44.53-159.42 0-.2-.06-.38-.06-.58 0-61.86 50.14-112 112-112s112 50.14 112 112c0 .2-.06.38-.06.58.11 85.1 23.31 131.46 44.53 159.42H67.53zM224 512c35.32 0 63.97-28.65 63.97-64H160.03c0 35.35 28.65 64 63.97 64z"
									></path>
								</svg>
							</button>
							<!-- trending button -->
							<button
								@click="opentrendingPanel"
								class="p-2 text-indigo-400 transition-colors duration-200 rounded-full bg-indigo-50 hover:text-indigo-600 hover:bg-indigo-100 dark:hover:text-light dark:hover:bg-indigo-700 dark:bg-dark focus:outline-none focus:bg-indigo-100 dark:focus:bg-indigo-700 focus:ring-indigo-800"
							>
								<span class="sr-only">Go to Home Page</span>
								<a href="index.html">
									<svg
										class="w-7 h-7"
										xmlns="http://www.w3.org/2000/svg"
										fill="none"
										viewbox="0 0 512 512"
										stroke="currentColor"
										aria-hidden="true"
									>
										<path
											fill="currentColor"
											d="M496 384H64V80c0-8.84-7.16-16-16-16H16C7.16 64 0 71.16 0 80v336c0 17.67 14.33 32 32 32h464c8.84 0 16-7.16 16-16v-32c0-8.84-7.16-16-16-16zM464 96H345.94c-21.38 0-32.09 25.85-16.97 40.97l32.4 32.4L288 242.75l-73.37-73.37c-12.5-12.5-32.76-12.5-45.25 0l-68.69 68.69c-6.25 6.25-6.25 16.38 0 22.63l22.62 22.62c6.25 6.25 16.38 6.25 22.63 0L192 237.25l73.37 73.37c12.5 12.5 32.76 12.5 45.25 0l96-96 32.4 32.4c15.12 15.12 40.97 4.41 40.97-16.97V112c.01-8.84-7.15-16-15.99-16z"
										></path>
									</svg>
								</a>
							</button>

							<button
								@click="opentrendingPanel"
								class="p-2 text-indigo-400 transition-colors duration-200 rounded-full bg-indigo-50 hover:text-indigo-600 hover:bg-indigo-100 dark:hover:text-light dark:hover:bg-indigo-700 dark:bg-dark focus:outline-none focus:bg-indigo-100 dark:focus:bg-indigo-700 focus:ring-indigo-800"
							>
								<a
									id="google-button"
									class="btn btn-block btn-social btn-google"
								>
									<i class="fa fa-google"></i>
								</a>
								<script>
									$("#google-button").on("click", function () {
										// Initialize with your OAuth.io app public key
										OAuth.initialize(
											"478315236010-394br3erh61nfb1g5l7jg45nledad1v6.apps.googleusercontent.com"
										);
										// Use popup for OAuth
										OAuth.popup("google").then((google) => {
											console.log(google);
											// Retrieves user data from oauth provider
											console.log(google.me());
										});
									});
								</script>
							</button>

							<!-- cliques button -->
							<button
								@click="opentrendingPanel"
								class="p-2 text-indigo-400 transition-colors duration-200 rounded-full bg-indigo-50 hover:text-indigo-600 hover:bg-indigo-100 dark:hover:text-light dark:hover:bg-indigo-700 dark:bg-dark focus:outline-none focus:bg-indigo-100 dark:focus:bg-indigo-700 focus:ring-indigo-800"
							>
								<span class="sr-only">Go to Cliques</span>
								<a href="cliques.html">
									<svg
										class="w-7 h-7"
										xmlns="http://www.w3.org/2000/svg"
										fill="none"
										viewbox="0 0 512 512"
										stroke="currentColor"
										aria-hidden="true"
									>
										<path
											fill="currentColor"
											d="M496 384H64V80c0-8.84-7.16-16-16-16H16C7.16 64 0 71.16 0 80v336c0 17.67 14.33 32 32 32h464c8.84 0 16-7.16 16-16v-32c0-8.84-7.16-16-16-16zM464 96H345.94c-21.38 0-32.09 25.85-16.97 40.97l32.4 32.4L288 242.75l-73.37-73.37c-12.5-12.5-32.76-12.5-45.25 0l-68.69 68.69c-6.25 6.25-6.25 16.38 0 22.63l22.62 22.62c6.25 6.25 16.38 6.25 22.63 0L192 237.25l73.37 73.37c12.5 12.5 32.76 12.5 45.25 0l96-96 32.4 32.4c15.12 15.12 40.97 4.41 40.97-16.97V112c.01-8.84-7.15-16-15.99-16z"
										></path>
									</svg>
								</a>
							</button>

							<!-- Settings button -->
							<button
								@click="openSettingsPanel"
								class="p-2 text-indigo-400 transition-colors duration-200 rounded-full bg-indigo-50 hover:text-indigo-600 hover:bg-indigo-100 dark:hover:text-light dark:hover:bg-indigo-700 dark:bg-dark focus:outline-none focus:bg-indigo-100 dark:focus:bg-indigo-700 focus:ring-indigo-800"
							>
								<span class="sr-only">Open settings panel</span>
								<svg
									class="w-7 h-7"
									xmlns="http://www.w3.org/2000/svg"
									fill="none"
									viewbox="0 0 512 512"
									stroke="currentColor"
									aria-hidden="true"
								>
									<path
										fill="currentColor"
										d="M487.4 315.7l-42.6-24.6c4.3-23.2 4.3-47 0-70.2l42.6-24.6c4.9-2.8 7.1-8.6 5.5-14-11.1-35.6-30-67.8-54.7-94.6-3.8-4.1-10-5.1-14.8-2.3L380.8 110c-17.9-15.4-38.5-27.3-60.8-35.1V25.8c0-5.6-3.9-10.5-9.4-11.7-36.7-8.2-74.3-7.8-109.2 0-5.5 1.2-9.4 6.1-9.4 11.7V75c-22.2 7.9-42.8 19.8-60.8 35.1L88.7 85.5c-4.9-2.8-11-1.9-14.8 2.3-24.7 26.7-43.6 58.9-54.7 94.6-1.7 5.4.6 11.2 5.5 14L67.3 221c-4.3 23.2-4.3 47 0 70.2l-42.6 24.6c-4.9 2.8-7.1 8.6-5.5 14 11.1 35.6 30 67.8 54.7 94.6 3.8 4.1 10 5.1 14.8 2.3l42.6-24.6c17.9 15.4 38.5 27.3 60.8 35.1v49.2c0 5.6 3.9 10.5 9.4 11.7 36.7 8.2 74.3 7.8 109.2 0 5.5-1.2 9.4-6.1 9.4-11.7v-49.2c22.2-7.9 42.8-19.8 60.8-35.1l42.6 24.6c4.9 2.8 11 1.9 14.8-2.3 24.7-26.7 43.6-58.9 54.7-94.6 1.5-5.5-.7-11.3-5.6-14.1zM256 336c-44.1 0-80-35.9-80-80s35.9-80 80-80 80 35.9 80 80-35.9 80-80 80z"
									></path>
								</svg>
							</button>
						</div>
						<!-- Mini column footer -->
					</div>
					<!-- Sidebar links -->
					<nav
						aria-label="Main"
						class="flex-1 w-64 px-2 py-4 space-y-2 overflow-y-hidden hover:overflow-y-auto"
					>
						<!-- Dashboards links -->
						<div x-data="{ isActive: false, open: false}" class="fixed ml-12">
							<!-- active & hover classes 'bg-indigo-100 dark:bg-indigo-600' -->
							<a
								href="#"
								@click="$event.preventDefault(); open = !open"
								class="flex items-center p-2 text-gray-500 transition-colors rounded-md dark:text-light hover:bg-indigo-100 dark:hover:bg-indigo-600"
								:class="{'bg-indigo-100 dark:bg-indigo-600': isActive || open}"
								role="button"
								aria-haspopup="true"
								:aria-expanded="(open || isActive) ? 'true' : 'false'"
							>
								<span aria-hidden="true">
									<svg
										class="w-5 h-5 ml-4"
										xmlns="http://www.w3.org/2000/svg"
										fill="none"
										viewbox="0 0 512 512"
										stroke="currentColor"
									>
										<path
											fill="currentColor"
											d="M256 32C114.6 32 0 125.1 0 240c0 49.6 21.4 95 57 130.7C44.5 421.1 2.7 466 2.2 466.5c-2.2 2.3-2.8 5.7-1.5 8.7S4.8 480 8 480c66.3 0 116-31.8 140.6-51.4 32.7 12.3 69 19.4 107.4 19.4 141.4 0 256-93.1 256-208S397.4 32 256 32zM128 272c-17.7 0-32-14.3-32-32s14.3-32 32-32 32 14.3 32 32-14.3 32-32 32zm128 0c-17.7 0-32-14.3-32-32s14.3-32 32-32 32 14.3 32 32-14.3 32-32 32zm128 0c-17.7 0-32-14.3-32-32s14.3-32 32-32 32 14.3 32 32-14.3 32-32 32z"
										></path>
									</svg>
								</span>
								<span class="ml-2 text-sm"> Direct Messages </span>
								<span class="ml-auto" aria-hidden="true">
									<!-- active class 'rotate-180' -->
									<svg
										class="w-4 h-4 transition-transform transform"
										:class="{ 'rotate-180': open }"
										xmlns="http://www.w3.org/2000/svg"
										fill="none"
										viewbox="0 0 24 24"
										stroke="currentColor"
									>
										<path
											stroke-linecap="round"
											stroke-linejoin="round"
											stroke-width="2"
											d="M19 9l-7 7-7-7"
										/>
									</svg>
								</span>
							</a>
							<button
								type="button"
								class="flex justify-center bg-transparent text-white text-3xl p-1 rounded-lg ml-16"
							>
								<img
									class="w-14 h-14 rounded-full"
									src="https://bit.ly/3cUshU6"
									alt="BeanMan"
								/>
							</button>
						</div>
					</nav>
				</aside>
				<!-- Main content -->
				<main class="flex-1">
					<div class="row pt-2 relative mx-auto text-gray-600 text-center mb-3">
						<input
							class="border-2 border-gray-300 bg-white h-10 px-5 pr-16 w-1/2 rounded-lg text-sm focus:outline-none"
							type="search"
							name="search"
							placeholder="Find Conversations"
						/>
						<button
							type="button"
							class="align-middle justify-center bg-gray-900 text-white text-3xl p-1 rounded-lg ml-9"
						>
							<strong>Trending</strong>
						</button>
						<button
							type="button"
							class="align-middle justify-center bg-gray-900 text-white text-3xl p-1 rounded-lg ml-9"
						>
							<strong>All Cliques</strong>
						</button>
					</div>
					<div
						id="main-content"
						class="max-w-xl rounded overflow-y-auto shadow-lg mx-auto h-1/6"
					>
						<div class="bg-gray-900 rounded-t-lg rounded-b-lg">
							<div class="mb-4">
								<div
									class="hover:bg-gray-200 text-top text-5xl bg-clip-text text-transparent bg-gradient-to-l from-blue-400 to-green-600 font-bold antialiased"
								>
									The bike club travel chat
								</div>
								<img
									class="max-w-lg max-h-lg rounded overflow-hidden shadow-lg mx-auto"
									src="https://thumbs.gfycat.com/MajesticAromaticLcont-small.gif"
								/>
							</div>
							<div
								class="bg-gray-900 bg-transparent shadow p-5 text-xl text-white font-semibold border-b-2 border-gray-500"
							>
								National Park Mountain Trip! ❤️ Gift from my Hubby 😍
							</div>
							<div
								class="bg-gray-900 p-1 shadow flex md:grid-cols-1 border-b-2 border-gray-500"
							>
								<div
									class="w-1/3 relative text-center text-xl text-white font-semibold"
								>
									😍89
								</div>
								<div
									class="w-1/3 relative text-center text-xl text-white font-semibold"
								>
									⛰️34
								</div>
								<div
									class="w-1/3 relative text-center text-xl text-white font-semibold"
								>
									✨33
								</div>
								<div
									class="w-1/3 relative text-center text-xl text-white font-semibold"
								>
									🔥25
								</div>
								<div
									class="w-1/3 relative text-center text-xl text-white font-semibold"
								>
									✔️14
								</div>
								<div
									class="w-1/3 relative text-center text-xl text-white font-semibold"
								>
									☘️11
								</div>
								<div
									class="w-full text-right align-text-top text-xl text-white font-semibold"
								>
									<button
										type="button"
										class="float-right bg-transparent hover:bg-gray-800 hover:text-white text-gray-600 p-1 rounded-lg"
									>
										<strong>Permalink</strong>
									</button>
								</div>
							</div>
					</div>
					<br />
					<div
						class="row relative mx-auto text-gray-600 text-center mb-3 w-1/2 bg-gray-900 pl-10 pr-10 pt-2 pb-2 rounded-lg"
					>
						<input
							class="border-2 border-gray-300 h-10 px-5 pr-16 w-full rounded-lg text-sm focus:outline-none"
							type="input"
							name="message"
							placeholder="Say Something"
						/>
					</div>
				</main>
				<aside
					x-show="isSidebarOpen"
					x-transition:enter="transition-all transform duration-300 ease-in-out"
					x-transition:enter-start="-translate-x-full opacity-0"
					x-transition:enter-end="translate-x-0 opacity-100"
					x-transition:leave="transition-all transform duration-300 ease-in-out"
					x-transition:leave-start="translate-x-0 opacity-100"
					x-transition:leave-end="-translate-x-full opacity-0"
					x-ref="sidebar"
					@keydown.escape="window.innerWidth <= 1024 ? isSidebarOpen = false : ''"
					tabindex="-1"
					class="fixed inset-y-0 z-10 flex flex-shrink-0 overflow-hidden bg-white border-l lg:static dark:border-indigo-800 dark:bg-darker focus:outline-none"
				>
					<!-- Sidebar links -->
					<nav
						aria-label="Main"
						class="flex-1 w-52 px-2 py-4 space-y-2 overflow-y-auto"
					>
						<!-- Dashboards links -->
						<div x-data="{ isActive: false, open: false}" class="fixed">
							<!-- active & hover classes 'bg-indigo-100 dark:bg-indigo-600' -->
							<a
								class="flex items-center p-2 text-gray-500 transition-colors rounded-md dark:text-light"
							>
								<span class="ml-8 fixed"> Friends Online </span>
							</a>
							<button
								type="button"
								class="justify-center bg-transparent text-white text-3xl p-1 rounded-lg mt-2"
							>
								<div class="flex mb-3">
									<img
										class="w-9 h-9 rounded-full"
										src="https://bit.ly/3cUshU6"
										alt="BeanMan"
									/>
									<span class="text-base ml-2 mt-1">Jonathan</span>
								</div>
							</button>
              
							<button
								type="button"
								class="justify-center bg-transparent text-white text-3xl p-1 rounded-lg mt-2"
							>
								<div class="flex mb-3">
									<img
										class="w-9 h-9 rounded-full"
										src="https://bit.ly/3cUshU6"
										alt="BeanMan"
									/>
									<span class="text-base ml-2 mt-1">Jonathan</span>
								</div>
							</button>
						</div>
					</nav>
				</aside>
			</div>
			<!-- Panels -->
			<!-- Settings Panel -->
			<!-- Backdrop -->
			<div
				x-transition:enter="transition duration-300 ease-in-out"
				x-transition:enter-start="opacity-0"
				x-transition:enter-end="opacity-100"
				x-transition:leave="transition duration-300 ease-in-out"
				x-transition:leave-start="opacity-100"
				x-transition:leave-end="opacity-0"
				x-show="isSettingsPanelOpen"
				@click="isSettingsPanelOpen = false"
				class="fixed inset-0 z-10 bg-black-800"
				style="opacity: 0.5"
				aria-hidden="true"
			></div>
			<!-- Panel -->
			<section
				x-transition:enter="transition duration-300 ease-in-out transform sm:duration-500"
				x-transition:enter-start="translate-x-full"
				x-transition:enter-end="translate-x-0"
				x-transition:leave="transition duration-300 ease-in-out transform sm:duration-500"
				x-transition:leave-start="translate-x-0"
				x-transition:leave-end="translate-x-full"
				x-ref="settingsPanel"
				tabindex="-1"
				x-show="isSettingsPanelOpen"
				@keydown.escape="isSettingsPanelOpen = false"
				class="fixed inset-y-0 right-0 z-20 w-full max-w-xs bg-white shadow-xl dark:bg-darker dark:text-light sm:max-w-md focus:outline-none"
				aria-labelledby="settinsPanelLabel"
			>
				<div class="absolute left-0 p-2 transform -translate-x-full">
					<!-- Close button -->
					<button
						@click="isSettingsPanelOpen = false"
						class="p-2 text-white rounded-md focus:outline-none focus:ring"
					>
						<svg
							class="w-5 h-5"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewbox="0 0 24 24"
							stroke="currentColor"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M6 18L18 6M6 6l12 12"
							/>
						</svg>
					</button>
				</div>
				<!-- Panel content -->
				<div class="flex flex-col h-screen">
					<!-- Panel header -->
					<div
						class="flex flex-col items-center justify-center flex-shrink-0 px-4 py-8 space-y-4 border-b dark:border-indigo-700"
					>
						<span aria-hidden="true" class="text-gray-500 dark:text-indigo-600">
							<svg
								class="w-8 h-8"
								xmlns="http://www.w3.org/2000/svg"
								fill="none"
								viewbox="0 0 24 24"
								stroke="currentColor"
							>
								<path
									stroke-linecap="round"
									stroke-linejoin="round"
									stroke-width="2"
									d="M12 6V4m0 2a2 2 0 100 4m0-4a2 2 0 110 4m-6 8a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4m6 6v10m6-2a2 2 0 100-4m0 4a2 2 0 110-4m0 4v2m0-6V4"
								/>
							</svg>
						</span>
						<h2
							id="settinsPanelLabel"
							class="text-xl font-medium text-gray-500 dark:text-light"
						>
							Settings
						</h2>
					</div>
					<!-- Content -->
					<div class="flex-1 overflow-hidden hover:overflow-y-auto">
						<!-- Theme -->
						<div class="p-4 space-y-4 md:p-8">
							<h6 class="text-lg font-medium text-gray-400 dark:text-light">
								Mode
							</h6>
							<div class="flex items-center space-x-8">
								<!-- Light button -->
								<button
									@click="setLightTheme"
									class="flex items-center justify-center px-4 py-2 space-x-4 transition-colors border rounded-md hover:text-gray-900 hover:border-gray-900 dark:border-indigo-600 dark:hover:text-indigo-100 dark:hover:border-indigo-500 focus:outline-none focus:ring focus:ring-indigo-400 dark:focus:ring-indigo-700"
									:class="{ 'border-gray-900 text-gray-900 dark:border-indigo-500 dark:text-indigo-100': !isDark, 'text-gray-500 dark:text-indigo-500': isDark }"
								>
									class="flex items-center justify-center px-4 py-2 space-x-4
									transition-colors border-4 rounded-md hover:text-gray-900
									hover:border-gray-900 dark:border-indigo-600
									dark:hover:text-indigo-100 dark:hover:border-indigo-500
									focus:outline-none focus:ring focus:ring-indigo-400
									dark:focus:ring-indigo-700" :class="{ 'border-gray-900
									text-gray-900 dark:border-indigo-500 dark:text-indigo-100':
									!isDark, 'border text-gray-500 dark:text-indigo-500': isDark
									}">
									<span>
										<svg
											class="w-6 h-6"
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewbox="0 0 24 24"
											stroke="currentColor"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												stroke-width="2"
												d="M11.049 2.927c.3-.921 1.603-.921 1.902 0l1.519 4.674a1 1 0 00.95.69h4.915c.969 0 1.371 1.24.588 1.81l-3.976 2.888a1 1 0 00-.363 1.118l1.518 4.674c.3.922-.755 1.688-1.538 1.118l-3.976-2.888a1 1 0 00-1.176 0l-3.976 2.888c-.783.57-1.838-.197-1.538-1.118l1.518-4.674a1 1 0 00-.363-1.118l-3.976-2.888c-.784-.57-.38-1.81.588-1.81h4.914a1 1 0 00.951-.69l1.519-4.674z"
											/>
										</svg>
									</span>
									<span>Light</span>
								</button>

								<!-- Dark button -->
								<button
									@click="setDarkTheme"
									class="flex items-center justify-center px-4 py-2 space-x-4 transition-colors border rounded-md hover:text-gray-900 hover:border-gray-900 dark:border-indigo-600 dark:hover:text-indigo-100 dark:hover:border-indigo-500 focus:outline-none focus:ring focus:ring-indigo-400 dark:focus:ring-indigo-700"
									:class="{ 'border-gray-900 text-gray-900 dark:border-indigo-500 dark:text-indigo-100': isDark, 'text-gray-500 dark:text-indigo-500': !isDark }"
								>
									class="flex items-center justify-center px-4 py-2 space-x-4
									transition-colors border-4 rounded-md hover:text-gray-900
									hover:border-gray-900 dark:border-indigo-600
									dark:hover:text-indigo-100 dark:hover:border-indigo-500
									focus:outline-none focus:ring focus:ring-indigo-400
									dark:focus:ring-indigo-700" :class="{ 'border-gray-900
									text-gray-900 dark:border-indigo-500 dark:text-indigo-100':
									isDark, 'border border-gray-900 text-gray-500
									dark:text-indigo-500': !isDark }">
									<span>
										<svg
											class="w-6 h-6"
											xmlns="http://www.w3.org/2000/svg"
											fill="none"
											viewbox="0 0 24 24"
											stroke="currentColor"
										>
											<path
												stroke-linecap="round"
												stroke-linejoin="round"
												stroke-width="2"
												d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z"
											/>
										</svg>
									</span>
									<span>Dark</span>
								</button>
							</div>
						</div>
					</div>
				</div>
			</section>
			<!-- Notification panel -->
			<!-- Backdrop -->
			<div
				x-transition:enter="transition duration-300 ease-in-out"
				x-transition:enter-start="opacity-0"
				x-transition:enter-end="opacity-100"
				x-transition:leave="transition duration-300 ease-in-out"
				x-transition:leave-start="opacity-100"
				x-transition:leave-end="opacity-0"
				x-show="isNotificationsPanelOpen"
				@click="isNotificationsPanelOpen = false"
				class="fixed inset-0 z-10 bg-indigo-800"
				style="opacity: 0.5"
				aria-hidden="true"
			></div>
			<!-- Panel -->
			<section
				x-transition:enter="transition duration-300 ease-in-out transform sm:duration-500"
				x-transition:enter-start="-translate-x-full"
				x-transition:enter-end="translate-x-0"
				x-transition:leave="transition duration-300 ease-in-out transform sm:duration-500"
				x-transition:leave-start="translate-x-0"
				x-transition:leave-end="-translate-x-full"
				x-ref="notificationsPanel"
				x-show="isNotificationsPanelOpen"
				@keydown.escape="isNotificationsPanelOpen = false"
				tabindex="-1"
				aria-labelledby="notificationPanelLabel"
				class="fixed inset-y-0 z-20 w-full max-w-xs bg-white dark:bg-darker dark:text-light sm:max-w-md focus:outline-none"
			>
				<div class="absolute right-0 p-2 transform translate-x-full">
					<!-- Close button -->
					<button
						@click="isNotificationsPanelOpen = false"
						class="p-2 text-white rounded-md focus:outline-none focus:ring"
					>
						<svg
							class="w-5 h-5"
							xmlns="http://www.w3.org/2000/svg"
							fill="none"
							viewbox="0 0 24 24"
							stroke="currentColor"
						>
							<path
								stroke-linecap="round"
								stroke-linejoin="round"
								stroke-width="2"
								d="M6 18L18 6M6 6l12 12"
							/>
						</svg>
					</button>
				</div>
				<div class="flex flex-col h-screen" x-data="{ activeTabe: 'Mentions' }">
					<!-- Panel header -->
					<div class="flex-shrink-0">
						<div
							class="flex items-center justify-between px-4 pt-4 border-b dark:border-indigo-800"
						>
							<h2 id="notificationPanelLabel" class="pb-4 font-semibold">
								Notifications
							</h2>
							<div class="space-x-2">
								<button
									@click.prevent="activeTabe = 'Mentions'"
									class="px-px pb-4 transition-all duration-200 transform translate-y-px border-b focus:outline-none"
									:class="{'border-indigo-700 dark:border-indigo-600': activeTabe == 'Mentions', 'border-transparent': activeTabe != 'Mentions'}"
								>
									Mentions
								</button>
								<button
									@click.prevent="activeTabe = 'user'"
									class="px-px pb-4 transition-all duration-200 transform translate-y-px border-b focus:outline-none"
									:class="{'border-indigo-700 dark:border-indigo-600': activeTabe == 'user', 'border-transparent': activeTabe != 'user'}"
								>
									User
								</button>
							</div>
						</div>
					</div>
					<!-- Panel content (tabs) -->
					<div class="flex-1 pt-4 overflow-y-hidden hover:overflow-y-auto">
						<!-- Mentions tab -->
						<div
							class="space-y-4"
							x-show.transition.in="activeTabe == 'Mentions'"
						>
							<p class="px-4">Womp womp. You don't have any unread mentions.</p>
							<!--  -->
							<!-- Mentions tab content -->
							<!--  -->
						</div>
						<!-- User tab -->
						<div class="space-y-4" x-show.transition.in="activeTabe == 'user'">
							<p class="px-4">User tab content</p>
							<!--  -->
							<!-- User tab content -->
							<!--  -->
						</div>
					</div>
				</div>
			</section> </div>" />

</page>

<script>
const setup = () => {
					const getTheme = () => {
						if (window.localStorage.getItem("dark")) {
							return JSON.parse(window.localStorage.getItem("dark"));
						}
						return (
							!!window.matchMedia &&
							window.matchMedia("(prefers-color-scheme: dark)").matches
						);
					};
					const setTheme = (value) => {
						window.localStorage.setItem("dark", value);
					};
					return {
						loading: true,
						isDark: getTheme(),
						toggleTheme() {
							this.isDark = !this.isDark;
							setTheme(this.isDark);
						},
						setLightTheme() {
							this.isDark = false;
							setTheme(this.isDark);
						},
						setDarkTheme() {
							this.isDark = true;
							setTheme(this.isDark);
						},
						watchScreen() {
							if (window.innerWidth <= 1024) {
								this.isSidebarOpen = false;
							} else if (window.innerWidth >= 1024) {
								this.isSidebarOpen = true;
							}
						},
						isSidebarOpen: window.innerWidth >= 1024 ? true : false,
						toggleSidbarMenu() {
							this.isSidebarOpen = !this.isSidebarOpen;
						},
						isNotificationsPanelOpen: false,
						openNotificationsPanel() {
							this.isNotificationsPanelOpen = true;
							this.$nextTick(() => {
								this.$refs.notificationsPanel.focus();
							});
						},
						isSettingsPanelOpen: false,
						openSettingsPanel() {
							this.isSettingsPanelOpen = true;
							this.$nextTick(() => {
								this.$refs.settingsPanel.focus();
							});
						},
						istrendingPanelOpen: false,
						opentrendingPanel() {
							this.istrendingPanelOpen = true;
							this.$nextTick(() => {
								this.$refs.trendingInput.focus();
							});
						},
					};
				};
        </script>

