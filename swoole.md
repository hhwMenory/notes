### 私密直播

#### 主播非私密直播

    1. 观众可以申请主播切换私密直播
    2. 主播端在私信列表查看用户申请
    3. 主播同意后推送 [主播切换私密] 通知 --- 全局推送

``` bash

    # /app/1/applyAnchorChangePriLive

    $owner = $this->getOwner();
    if ($owner->livestatus != 1) {

        return $this->json(0, '');

    }

    if ($owner->live_type === 'private') {

        return $this->json(0, '');

    }

    $applyAnchorChangePriLiveKey = RoomLiving::getApplyAnchorChangePriLiveKey();

    $rank = $this->redis->zRank($applyAnchorChangePriLiveKey, $owner->id);

    if ($rank > 0) {

        // 不能重复申请

    }

    $this->redis->zAdd($applyAnchorChangePriLiveKey, time(), $owner->id);

    # /app/1/dealAnchorChangePriLiveApply?uid=10492&result=agree

    user string anchor_changer_pri_live_apply_status_rid_uid => [1 | -1]

```

#### 主播已私密直播

    1. 观众可以申请主播切换私密直播
    2. 主播端在私信列表查看用户申请
    3. 主播同意后推送 [主播同意用户观看私密直播] 通知


``` bash


```



``` bash

    function userAgent() {
        var u = navigator.userAgent.toLowerCase();
        if(isWeiXin()){
            if (u.indexOf('android') > -1 || u.indexOf('linux') > -1) {//安卓手机
                $("#imgtip").show();
                $("#imgtip").attr("src", "/images/androdtips.png");
            } else if (u.indexOf('iphone') > -1) {//苹果手机
                $("#imgtip").show();
                $("#imgtip").attr("src", "/images/appletips.png");
            }
        }else{
            if(u.toLowerCase().indexOf('iphone')>-1||u.toLowerCase().indexOf('ipad')>-1){
                window.location.href = "itms-apps://itunes.apple.com/app/id1148831953";
            }else{
                window.location.href = "http://bobo.aaniao.com/download/down/boboapp.apk";
                //document.write("安卓版本正在开发，敬请期待！");
            }
        }
    }

    function isWeiXin() {
        var ua = window.navigator.userAgent.toLowerCase();
        if (ua.match(/MicroMessenger/i) == 'micromessenger') {
            return true;
        } else {
            return false;
        }
    }

```


``` bash

/**
 * @todo 获取用户申请
 * @author menory
 */
public function getUserApplysAction() {

    $page     = $this->request->get('page', 'int', 1);
    $pagesize = $this->request->get('pagesize', 'int', 1);

    $owner = $this->getOwner();
    
    if ($owner->livestatus != 1) {

        // 不在直播

    }
    
    if ($owner->live_private == 'private') {

        // 进入观看申请

    } else {
    
        // 主播切换私密直播申请
        $applyKey = RoomLiving::getApplyAnchorChangePriLiveKey($owner->id);
        
    }

    $applyData = $this->redis->zRevRange($applyKey, 0, $pagesize); // 分页

    $result = [];
    if (!empty($applyData)) {

        // $users = User::query()
        //     ->where('id IN({ids:array})', ['ids' => $applyData])
        //     ->execute();

        // foreach ($users as $user) {
        //     $result[] = [
        //         'uid'     => $user->id,
        //         'nick'    => $user->nick,
        //         'avatar'  => $user->avatar,
        //         'richlvl' => $user->richlvl,
        //     ];
        // }

        // $pipe = $this->redis->multi(Redis::PIPELINE);
        // foreach ($applyData as $uid => $time) {
        //     $infoKey = RoomLiving::getInfoKey($owner->id, $uid);
        //     $pipe->hGetAll($infoKey);
        // }
        // $replies = $pipe->exec();

        // $i = 0;
        // foreach ($applyData as $uid => $score) {
        //     $user = $replies[$i++];
        //     if (empty($user)) {
        //         continue;
        //     }
        //     $result[] = [
        //         'uid'     => $uid,
        //         'nick'    => $user['nick'],
        //         'avatar'  => $user['avatar'],
        //         'richlvl' => $user['richlvl'],
        //     ];
        // };

    }

    $this->json(1, 'successful', $result);

}


/**
 * 用户申请主播切换为私密直播
 * @author menory
 */
public function applyAnchorChangePriLiveAction() {

    $rid = $this->request->get('rid', 'int');

    if (empty($rid)) {

        return $this->json(20001, 'param', '', ['param' => 'rid']);

    }

    $owner = $this->getOwner();

    $anchor = User::findOne($rid, 0, true);

    if ($anchor->livestatus != 1) {

        return $this->json(0, 'liveundefined');

    }

    if ($owner->live_type === 'private') {

        return $this->json(0, '');

    }

    $applyAnchorChangePriLiveKey = RoomLiving::getApplyAnchorChangePriLiveKey($rid);
    
    $rank = $this->redis->zRank($applyAnchorChangePriLiveKey, $owner->id);

    if ($rank !== false) {

        // 不能重复申请
        return $this->json(0, 'applyisexit');

    }

    $isZAdd = $this->redis->zAdd($applyAnchorChangePriLiveKey, time(), $owner->id);

    if ($isZAdd !== false) {

        $notify = [
            'type' => 'apply_anchor_change_pri_live',
            'data' =>[
                'fuser' => $owner->getInfo()
            ]
        ];
        $this->notify($notify, $owner->id);

        return $this->json(1, 'successful');

    } else {

        return $this->json(0, 'failure');

    }

}

### 主播切换私密
  
    - live_price=100
    - uids=1,2,3,4,5
    
    if (!empty($livePrice)) {

        // 验证价格

    } else {
    
        $livePrice = min

    }

    if (!empty($uids)) {

        $uids = explode(',', trim(',', $uids));
        
        foreach ($uids as $id) {
            // 生成申请进入成功信息

        }

    }

    // 推送可以进入的用户 ID

    // 清除申请信息
    $this->redis->del(RoomLiving::getApplyAnchorChangePriLiveKey($owner->id));




```
