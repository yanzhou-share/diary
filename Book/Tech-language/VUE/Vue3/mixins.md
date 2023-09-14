# vue3中mixins的用法
```javascript
// maxins.js content
export default function getHomeMixin() {
    const router = useRouter();

    function gotoPersonal(uid) {
        router.push({ name: 'personalHomePage' });
    }

    return { gotoPersonal };
}

// 引入的用法
improt getHomeMixin from 'index'
const mix = getHomeMixin()
```