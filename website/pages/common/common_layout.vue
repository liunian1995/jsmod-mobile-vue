<template>
	<div id="common-layout">
		<common-header v-bind:onRigthBtn="onRigthBtn" v-if="showHeader" v-bind:hideBack="hideBack" v-bind:title="title" v-bind:OrderTip="OrderTip" v-bind:isService="isService" v-bind:isTitle="isTitle">
      <span v-if="rightBtn" v-html="rightBtn"></span>
		</common-header>

    <div v-if="showSource" class="common-footer-source">
      <a :href="'https://github.com/chaogao/jsmod-mobile-vue/tree/master/website/pages/' + source ">
        <span>本例源码</span>
        <i class="iconjsmod iconjsmod-xiangyou1"></i>
      </a>
    </div>

		<slot v-if="isShowNotFound" name="header">
			<common-header v-bind:title="'找不到页面'"></common-header>
		</slot>

		<div v-if="!isShowNotFound" v-bind:style="{minHeight: this.winHeight + 'px'}" v-bind:class="['container', containerClass, {'has-footer': !hideFooter}]">
			<slot></slot>
		</div>

		<slot v-if="!isShowNotFound" name="footer">
			<common-footer :source="source" v-if="!hideFooter" v-bind:footerTab="footerTab"></common-footer>
		</slot>
	</div>
</template>

<script>
import CommonHeader from './common_header';
import CommonFooter from './common_footer';

export default {
	name: 'common-layout',
	data () {
		return {
			winHeight: this.containerClass == 'container-gray' ? (window.outerHeight || window.innerHeight) - 45 : 0
		}
	},

	props: ['title', 'hideFooter', 'containerClass', 'isShowNotFound', 'footerTab', 'hideBack', 'rightBtn', 'onRigthBtn', 'OrderTip', 'isService', 'isTitle', 'source'],

  computed: {
    showHeader () {
      let inIframe = window.location.href.indexOf('iframe') > 0;

      return !inIframe;
    },

    showSource () {
      let inIframe = window.location.href.indexOf('iframe') > 0;

      return !inIframe && this.source;
    }
  },

	components: {
		CommonHeader,
		CommonFooter
	}
}
</script>

<style scoped lang="stylus">
	#common-layout
	.container {
		&.container-gray {
			background: #EAEAEA;
		}

		&.has-footer {
			// padding-bottom: 120px;
		}
	}


	.fade-leave {
		display: none;
	}

	.fade-leave-active {
		display: none;
	}

	.fade-enter-active {
		transition: opacity 1s;

		.container {
			transition: opacity 1s;
			opacity: 1;
		}
	}

	.fade-enter {
		transition: opacity 1s;

		.container {
			transition: opacity 1s;
			opacity: 0;
		}
	}


  .common-footer-source {
    margin-bottom: 5px;

    a {
      background: #efefef;
      color: #999;
      text-align: left;
      display: block;
      padding: 10px;
    }

    i {
      float: right;
      margin-top: 3px;
    }
  }
</style>
