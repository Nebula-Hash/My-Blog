<template>
  <footer id="footer">
    <div id="footer_icons" class="myCenter">
      <a class="icon_link myCenter" target="_blank" rel="noopener" href="https://github.com/Nebula-Hash"
        title="Github主页">
        <SvgIcon icon="GitHubIcon" size="24px" />
      </a>
      <a class="icon_link myCenter" target="_blank" rel="noopener" href="https://gitee.com" title="Gitee主页">
        <SvgIcon icon="GiteeIcon" size="24px" />
      </a>
      <img class="footer_logo entered loaded" src="/images/nebula-hash.jpg" data-lazy-src="/images/nebula-hash.jpg"
        data-ll-status="loaded" @click="toUrl('/about')" title="个人主页" style="cursor: pointer;" />
      <a class="icon_link myCenter" target="_blank" rel="noopener" href="https://blog.csdn.net" title="CSDN主页">
        <SvgIcon icon="CSDNIcon" size="24px" />
      </a>
      <a class="icon_link myCenter" target="_blank" rel="noopener" href="https://leetcode.cn" title="LeetCode主页">
        <SvgIcon icon="LeetCodeIcon" size="24px" />
      </a>
    </div>

    <div id="footer-bottom">
      <div class="footer-bottom-content">
        <div class="footer-bottom-left">
          <span>Copyright © 2023 By
            <a data-pjax-state="" href="javascript:;" @click="toUrl('/')" :title="`点击访问${constant.siteName}的主页`">{{
              constant.siteName }}
            </a>
          </span>
          <div>
            <a class="footer-bottom-link" target="_blank" href="https://cloud.tencent.com/"
              title="腾讯云提供图片存储和网站托管">腾讯云</a>
            <a class="footer-bottom-link" target="_blank" href="https://tongji.baidu.com/" title="百度统计提供用户访问统计">百度统计</a>
            <a class="footer-bottom-link" target="_blank" href="https://vercel.com/" title="Vercel提供镜像站托管">Vercel</a>
            <a class="footer-bottom-link" target="_blank" href="https://github.com/" title="Github提供源码托管">Github</a>
          </div>
        </div>
        <div class="footer-bottom-right">
          <div id="runtime">本站已运行：{{ countdownChange }}</div>
          <div>
            <a class="footer-bottom-link" target="_blank" href="https://v2.cn.vuejs.org/v2/guide/" title="框架">Vue3</a>
            <a class="footer-bottom-link" target="_blank" href="https://docs.djangoproject.com/zh-hans/5.0/"
              title="框架">Django</a>
            <a class="footer-bottom-link" href="javascript:;" title="备案号">京cpu备5201314号</a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from "vue";
import { useGlobalProperties } from "@/composables/useGlobalProperties";
import { useRouter } from "vue-router";
import constant from "@/utils/constant";
import SvgIcon from "@/components/SvgIcon.vue";

const router = useRouter();
const { $common } = useGlobalProperties();

const countdownTime = ref<string>("2026-04-06 00:00:00");
const countdownChange = ref<string>("");
const countdownTimer = ref<ReturnType<typeof setInterval> | null>(null);

onMounted(() => {
  countdownTimer.value = setInterval(() => {
    countdown();
  }, 1000);
});

onBeforeUnmount(() => {
  if (countdownTimer.value) {
    clearInterval(countdownTimer.value);
    countdownTimer.value = null;
  }
});

const toUrl = (path: string): void => {
  router.push(path);
};

const countdown = (): void => {
  if ($common.isEmpty(countdownTime.value)) {
    return;
  }
  const countdownResult = $common.countdown(countdownTime.value);
  countdownChange.value =
    countdownResult.d +
    "天" +
    countdownResult.h +
    "时" +
    countdownResult.m +
    "分" +
    countdownResult.s +
    "秒";
  countdownChange.value = countdownChange.value.replace(/-/g, " ");
};
</script>

<style lang="scss" scoped>
#footer_icons {
  margin: auto;
  background: var(--background);
}

#footer_icons {
  padding-top: 2rem;
  padding-bottom: 1rem;
  flex-wrap: wrap;
  gap: 1rem;

  img.footer_logo {
    border-style: none;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    margin: 0 1rem;
    filter: drop-shadow(0 0 12px var(--blue22));
    transition: all 0.25s;

    &:hover {
      transform: scale(1.1);
      transition-duration: 0.4s;
    }
  }

  a {
    text-decoration: none;
    word-wrap: break-word;
    transition: all 0.2s;
    overflow-wrap: break-word;
  }

  .icon_link {
    height: 40px;
    width: 40px;
    background-color: rgba(0, 0, 0, 0.3);
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: all 0.3s ease;
    backdrop-filter: blur(5px);

    :deep(.svg-icon) {
      opacity: 0.85;
      filter: brightness(1.2) contrast(1.1) drop-shadow(0 1px 2px rgba(0, 0, 0, 0.2));
      transition: all 0.3s ease;
    }

    i {
      font-size: 20px;
      color: var(--favoriteBg);
    }

    &:hover {
      background: var(--red);
      transform: scale(1.1);

      :deep(.svg-icon) {
        opacity: 1;
        filter: brightness(1.3) contrast(1.2) drop-shadow(0 2px 4px rgba(0, 0, 0, 0.3));
      }
    }
  }
}

#footer-bottom {
  padding: 1rem;
  background: var(--background);
  z-index: 2;

  .footer-bottom-content {
    display: flex;
    justify-content: space-between;
    max-width: 1100px;
    width: 100%;
    margin: 0 auto;
    flex-wrap: wrap;
  }

  .footer-bottom-left {
    a {
      margin-left: 5px;
    }
  }

  .footer-bottom-left,
  .footer-bottom-right {
    display: flex;
    flex-direction: column;
  }

  .footer-bottom-content * {
    font-size: 17px;
    white-space: nowrap;
    color: var(--fontColor);
  }

  .footer-bottom-left div,
  .footer-bottom-right div,
  .footer-bottom-left span,
  .footer-bottom-right span {
    display: flex;
    align-items: center;
  }

  a {
    display: flex;
    align-items: center;

    &:not(:first-child)::before {
      content: "|";
      font-size: 14px;
      line-height: 2.45;
      margin: 0 10px;
    }

    &:hover {
      color: var(--red);

      &:not(:first-child)::before {
        color: var(--fontColor);
      }
    }
  }

  .footer-bottom-right div {
    justify-content: flex-end;
  }
}

@media screen and (max-width: 768px) {
  #footer-bottom {
    padding: 1rem 0;

    .footer-bottom-content * {
      font-size: 1rem;
    }

    .footer-bottom-left,
    .footer-bottom-right {
      width: 100%;
      align-items: center;
    }
  }

  #footer_icons img.footer_logo {
    display: none;
  }
}
</style>
