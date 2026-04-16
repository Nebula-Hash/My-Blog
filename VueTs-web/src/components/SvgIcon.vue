<template>
    <img :src="iconSrc" :alt="icon" :class="['svg-icon', customClass]" :style="{ width: size, height: size }" />
</template>

<script setup lang="ts">
import { computed } from 'vue';

// 技术平台图标
import GitHubIcon from '@/assets/svg/tech-icons/GitHub.svg';
import GiteeIcon from '@/assets/svg/tech-icons/Gitee.svg';
import CSDNIcon from '@/assets/svg/tech-icons/CSDN.svg';
import LeetCodeIcon from '@/assets/svg/tech-icons/LeetCode.svg';

// 社交媒体图标
import WeChatIcon from '@/assets/svg/social-media-icons/WeChat.svg';
import QQIcon from '@/assets/svg/social-media-icons/QQ.svg';
import BiLiBiLiIcon from '@/assets/svg/social-media-icons/BiLiBiLi.svg';
import XiaoHongShuIcon from '@/assets/svg/social-media-icons/XiaoHongShu.svg';
import DouYinIcon from '@/assets/svg/social-media-icons/DouYin.svg';
import ZhiHuIcon from '@/assets/svg/social-media-icons/ZhiHu.svg';
import QQMusicIcon from '@/assets/svg/social-media-icons/QQMusic.svg';

interface Props {
    icon: 'GitHubIcon' | 'GiteeIcon' | 'CSDNIcon' | 'LeetCodeIcon' |
    'WeChatIcon' | 'QQIcon' | 'BiLiBiLiIcon' | 'XiaoHongShuIcon' |
    'DouYinIcon' | 'ZhiHuIcon' | 'QQMusicIcon';
    size?: string;
    customClass?: string;
}

const props = withDefaults(defineProps<Props>(), {
    size: '1em',
    customClass: ''
});

const iconMap: Record<string, string> = {
    GitHubIcon,
    GiteeIcon,
    CSDNIcon,
    LeetCodeIcon,
    WeChatIcon,
    QQIcon,
    BiLiBiLiIcon,
    XiaoHongShuIcon,
    DouYinIcon,
    ZhiHuIcon,
    QQMusicIcon,
};

const iconSrc = computed(() => {
    return iconMap[props.icon] || '';
});
</script>

<style scoped>
.svg-icon {
    display: inline-block;
    vertical-align: middle;
}
</style>
