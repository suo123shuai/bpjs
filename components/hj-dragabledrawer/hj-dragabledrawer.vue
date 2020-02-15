<template>
	<!-- #ifndef H5 -->
	<view :animation="animationData" class="uni-drawer" :class="{'uni-drawer-visible':visible,'uni-drawer-right':option.rightMode}">
		<!-- #endif -->
		<!-- #ifdef H5 -->
		<view :id="id" class="uni-drawer" :class="{'uni-drawer-visible':visible,'uni-drawer-right':option.rightMode}">
			<!-- #endif -->
			<!-- #ifndef APP-PLUS -->
			<view v-if="showmask" class="uni-drawer-mask" @tap.stop="close(0)" @touchmove.stop="stopref" @touchend="stopref"></view>
			<!-- #endif -->
			<!-- #ifdef APP-PLUS -->
			<view v-if="showmask" class="uni-drawer-mask" @tap.stop="close(0)"></view>
			<!-- #endif -->
			<view class="uni-drawer-content" @touchstart="updateStart" @touchmove.stop="updateMove" @touchend="updateEnd" :style="{width:option.width+'%'}">
				<slot></slot>
			</view>
		</view>
</template>

<script>
	let updating = false;
	export default {
		name: 'hj-dragabledrawer',
		props: {
			/**
			 * 显示状态
			 */
			options: Object
		},
		data() {
			return {
				def: {
					rightMode: true,
					mask: true,
					width: 60,
					autoClose: true
				},
				// #ifdef H5
				id: 'hj-draw' + Date.now(),
				drawer: null,
				// #endif
				// #ifndef H5
				animationData: {},
				// #endif
				show: true,
				visible: false
			}
		},
		computed: {
			option: function() {
				return { ...this.def,
					...this.options
				}
			},
			showmask: function() {
				return this.option.mask && this.show
			}
		},
		created() {
			try {
				// #ifdef APP-PLUS
				const pages = getCurrentPages();
				const page = pages[pages.length - 1];
				const currentWebview = page.$getAppWebview();
				currentWebview.setStyle({
					pullToRefresh: {
						support: false
					}
				});
				// #endif
				// #ifndef H5
				this.animation = uni.createAnimation();
				// #endif
				this.screenWidth = uni.getSystemInfoSync().windowWidth;
				// #ifdef H5
				setTimeout(() => {
					this.drawer = document.getElementById(this.id);
				}, 100)
				// #endif
			} catch (e) {
				this.$emit("error", e)
			}
		},
		methods: {
			open() {
				this.visible = true;
				this.$emit("open", {
					success: 1
				})
			},
			close(force = 1) {
				if (force || this.option.autoClose) {
					this.visible = false;
					// #ifdef H5
					setTimeout(() => {
						this.drawer.style.left = "0px"
						this.$emit("close", {
							success: 1
						})
					}, 500)
					// #endif
					// #ifndef H5
					this.$emit("close", {
						success: 1
					})
					// #endif
				}
			},
			updateStart: function(e) {
				this.start = e.touches[0].pageX;
				this.scale = this.screenWidth / (this.screenWidth - this.start)
			},
			async updateMove(e) {
				if (updating) return
				updating = true;
				// #ifndef APP-PLUS|| H5
				this.stopref()
				// #endif
				this.tx = this.scale * (e.touches[0].pageX - this.start);
				this.show = false;
				// #ifndef H5
				if (this.option.rightMode) {
					if (this.tx > 0) {
						this.animation.translateX(this.tx).step({
							duration: 100
						})
					}
				} else {
					if (this.tx < 0) {
						this.animation.translateX(this.tx).step({
							duration: 100
						})
					}
				}
				this.animationData = this.animation.export()
				// #endif
				// #ifdef H5
				e.preventDefault()
				if (this.option.rightMode) {
					if (this.tx > 0) {
						this.drawer.style.left = this.tx + "px"
					}
				} else {
					if (this.tx < 0) {
						this.drawer.style.left = this.tx + "px"
					}
				}
				// #endif
				updating = false
			},
			// #ifdef H5
			rev: function() {
				var left = parseInt(this.drawer.style.left);
				if (left > 0) {
					if (left > 10) {
						setTimeout(() => {
							this.drawer.style.left = left - 10 + 'px';
							this.rev()
						}, 10)
					} else {
						setTimeout(() => {
							this.drawer.style.left = '0px'
						}, 10)
					}
				} else {
					if (left < -10) {
						setTimeout(() => {
							this.drawer.style.left = left + 10 + 'px';
							this.rev()
						}, 10)
					} else {
						setTimeout(() => {
							this.drawer.style.left = '0px'
						}, 10)
					}
				}
			},
			// #endif
			updateEnd: function() {
				this.show = true;
				// #ifndef APP-PLUS|| H5
				this.stopref();
				// #endif
				// #ifndef H5
				if (this.option.rightMode) {
					if (this.tx > 100) {
						this.close()
					}
				} else {
					if (this.tx < -80) {
						this.close()
					}
				}
				this.animation.translateX(0).step();
				this.animationData = this.animation.export();
				// #endif
				// #ifdef H5
				if (this.option.rightMode) {
					if (this.tx > 100) {
						this.close()
					} else {
						this.rev()
					}
				} else {
					if (this.tx < -80) {
						this.close()
					} else {
						this.rev()
					}
				}
				// #endif
				this.tx=0
			},
			stopref: uni.stopPullDownRefresh
		}
	}
</script>

<style scoped>
	.uni-drawer {
		display: block;
		position: fixed;
		/* #ifndef H5 */
		top: 0;
		/* #endif */
		/* #ifdef H5 */
		top: var(--window-top);
		/* #endif */
		left: 0;
		width: 750upx;
		bottom: 0;
		overflow: hidden;
		visibility: hidden;
		z-index: 99;
	}

	.uni-drawer>.uni-drawer-mask {
		display: block;
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background: rgba(0, 0, 0, 0.4);
	}

	.uni-drawer>.uni-drawer-content {
		display: block;
		position: absolute;
		top: 0;
		left: 0;
		height: 100%;
		background: #FFFFFF;
		transition: all 0.3s ease-out;
		transform: translatex(-100%);
	}

	.uni-drawer.uni-drawer-right>.uni-drawer-content {
		left: auto;
		right: 0;
		transform: translatex(100%);
	}

	.uni-drawer.uni-drawer-visible {
		visibility: visible;
	}

	.uni-drawer.uni-drawer-visible>.uni-drawer-mask {
		display: block;
	}

	.uni-drawer.uni-drawer-visible>.uni-drawer-content {
		transform: translatex(0);
	}
</style>
