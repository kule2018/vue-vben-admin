<!--
 * @description:
 * @author: wenbin.chen
 * @Date: 2020-05-25 16:21:40
 * @LastEditors: wenbin.chen
 * @LastEditTime: 2020-06-17 11:30:48
 * @email: 190848757@qq.com
-->

<script lang="tsx">
  import { Breadcrumb } from 'ant-design-vue';
  import { defineComponent, computed, unref } from '@vue/composition-api';

  import { useDesign } from '@/hooks/core/useDesign';
  import { menuStore } from '@/store/modules/menu';

  export default defineComponent({
    name: 'LayoutBread',
    setup() {
      const { prefixCls } = useDesign('layout-bread');

      const getBreadcrumbList = computed(() => {
        return menuStore.getCurrMenuState;
      });

      return () => (
        <Breadcrumb class={prefixCls}>
          {(unref(getBreadcrumbList) || []).map((item) => {
            return (
              <Breadcrumb.Item href={item.path} key={item.path} separator="/">
                <router-link to={{ path: item.path === '' ? '/' : item.path }}>
                  {item.name}
                </router-link>
              </Breadcrumb.Item>
            );
          })}
        </Breadcrumb>
      );
    },
  });
</script>
<style scoped lang="less">
  @import (reference) '~@design';
  @prefix-cls: ~'@{namespace}-layout-bread';

  .@{prefix-cls} {
    padding: 8px;
    background: @white;
  }

  // .breadcrumb-enter-active,
  // .breadcrumb-leave-active {
  //   transition: all 0.5s;
  // }

  // .breadcrumb-enter,
  // .breadcrumb-leave-active {
  //   opacity: 0;
  //   transform: translateX(-20px);
  // }

  // .breadcrumb-move {
  //   transition: all 0.5s;
  // }

  // .breadcrumb-leave-active {
  //   position: absolute;
  // }
</style>
