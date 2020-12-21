# void-OWO ——VOID 主题增加自定义表情包
typecho博客评论表情包升级
【转载保存】原文链接：https://blog.catyo.cn/archives/2044/

## 一、准备资源
下载表情包上传到主题目录
存放路径：`博客根目录/usr/themes/VOID/assets/libs/owo/biaoqing`

## 二、修改文件
### ① OwO_02.json
`博客根目录/usr/themes/VOID/assets/libs/owo/biaoqing/OwO_02.json` ，直接修改/替换

 修改后的 `OwO_02.json` 文件，参考json规范
```
{
  "维尼": { ...
  "蛆音娘": { ...
  "阿鲁": { ...
  "哔哩": { ...
  "微博": { ...
  "泡泡": { ...
  "热门": { ...
}
```
### ② Contents.php
`博客根目录/usr/themes/VOID/libs/Contents.php` 中找到解析表情方法 `parseBiaoQing`，在原有的 `parseQuyinBiaoqingCallback` 下添加四个函数，并分别新增四个函数的表情回调方法。

修改 `Contents.php` 文件，大概在184行左右
```
/**
 * 解析表情
 *
 * @return string
 */
static public function parseBiaoQing($content)
{
  $content = preg_replace_callback('/\:\:\(\s*(呵呵|哈哈|吐舌|太开心|笑眼|花心|小乖|乖|捂嘴笑|滑稽|你懂的|不高兴|怒|汗|黑线|泪|真棒|喷|惊哭|阴险|鄙视|酷|啊|狂汗|what|疑问|酸爽|呀咩爹|委屈|惊讶|睡觉|笑尿|挖鼻|吐|犀利|小红脸|懒得理|勉强|爱心|心碎|玫瑰|礼物|彩虹|太阳|星星月亮|钱币|茶杯|蛋糕|大拇指|胜利|haha|OK|沙发|手纸|香蕉|便便|药丸|红领巾|蜡烛|音乐|灯泡|开心|钱|咦|呼|冷|生气|弱|吐血)\s*\)/is',
      array('Contents', 'parsePaopaoBiaoqingCallback'), $content);
  $content = preg_replace_callback('/\:\@\(\s*(高兴|小怒|脸红|内伤|装大款|赞一个|害羞|汗|吐血倒地|深思|不高兴|无语|亲亲|口水|尴尬|中指|想一想|哭泣|便便|献花|皱眉|傻笑|狂汗|吐|喷水|看不见|鼓掌|阴暗|长草|献黄瓜|邪恶|期待|得意|吐舌|喷血|无所谓|观察|暗地观察|肿包|中枪|大囧|呲牙|抠鼻|不说话|咽气|欢呼|锁眉|蜡烛|坐等|击掌|惊喜|喜极而泣|抽烟|不出所料|愤怒|无奈|黑线|投降|看热闹|扇耳光|小眼睛|中刀)\s*\)/is',
      array('Contents', 'parseAruBiaoqingCallback'), $content);
  $content = preg_replace_callback('/\:\&\(\s*(.*?)\s*\)/is',
      array('Contents', 'parseQuyinBiaoqingCallback'), $content);
  $content = preg_replace_callback('/\:\#\(\s*(.*?)\s*\)/is',
      array('Contents', 'parseAruNewBiaoqingCallback'), $content);
  $content = preg_replace_callback('/\:\$\(\s*(.*?)\s*\)/is',
      array('Contents', 'parseBilibiliBiaoqingCallback'), $content);
  $content = preg_replace_callback('/\:\^\(\s*(.*?)\s*\)/is',
      array('Contents', 'parseWeiboBiaoqingCallback'), $content);
  $content = preg_replace_callback('/\:\!\(\s*(.*?)\s*\)/is',
      array('Contents', 'parseWinnieBiaoqingCallback'), $content);
  $content = preg_replace_callback('/\:\%\(\s*(.*?)\s*\)/is',
      array('Contents', 'parseWeisuoBiaoqingCallback'), $content);
        return $content;
  return $content;
}
```
   
```
/**
 * 新版阿鲁表情回调函数
 *
 * @return string
 */
private static function parseAruNewBiaoqingCallback($match)
{
    return '<img class="biaoqing" src="/usr/themes/VOID/assets/libs/owo/biaoqing/arunew/'. str_replace('%', '', urlencode($match[1])) . '.png">';
}

/**
 * Bilibili表情回调函数
 *
 * @return string
 */
private static function parseBilibiliBiaoqingCallback($match)
{
    return '<img class="biaoqing" src="/usr/themes/VOID/assets/libs/owo/biaoqing/bilibili/'. str_replace('%', '', urlencode($match[1])) . '.png">';
}

/**
 * Weibo表情回调函数
 *
 * @return string
 */
private static function parseWeiboBiaoqingCallback($match)
{
    return '<img class="biaoqing" src="/usr/themes/VOID/assets/libs/owo/biaoqing/weibo/'. str_replace('%', '', urlencode($match[1])) . '.png">';
}

/**
 * 维尼表情回调函数
 *
 * @return string
 */
private static function parseWinnieBiaoqingCallback($match)
{
    return '<img class="biaoqing" src="/usr/themes/VOID/assets/libs/owo/biaoqing/winnie/'. str_replace('%', '', urlencode($match[1])) . '.png">';
}

 /**
     * 热门表情表情回调函数
     * 
     * @return string
     */
    private static function parseWeisuoBiaoqingCallback($match)
    {
        return '<img class="biaoqing" src="/usr/themes/VOID/assets/libs/owo/biaoqing/weisuo/'. str_replace('%', '', urlencode($match[1])) . '.gif">';
    }
```
