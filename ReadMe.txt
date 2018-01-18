




































sys
orcl




mstsc /admin /v:目标ip



192.168.0.211   
218.2.135.1                    

 淡奶油250克，牛奶250克，炼乳35克，糖20克，香草夹三分之一根，全蛋1个，蛋黄4个

全蛋和蛋黄混合均匀，其他材料混合后加热到糖全部融化，放到微温倒进蛋液里，混合均匀，过筛两次
然后倒进碗里，烤箱用水浴法，140度烤20到30分钟，看看表面想果冻那样就可以了



http://www.open-open.com/lib/view/open1354515766351.html


王成友 08:36:03
http://newb2c.coseo.cn/admin/login.aspx


http://localhost/zzgz/Content/css/bootstrap.min14ed.css?v=3.3.6



双轮  普通版是980  升级版是1350 .运动铂金款是2480 眼部专用款是780 


http://www.cnblogs.com/artwl/archive/2012/03/31/2427019.html






配方很简单
蛋黄3个，淡奶油250ML，你喜欢的任意水果150克到200克
细砂糖40克



蛋黄+糖，隔着40度热水打发成丝带状，后期再把热水加热到80度，再打一会，我一般不后期加热
然后淡奶油打到6分发左右，浓稠即可
两者用打蛋器混合
然后急冻就可以了
就是这个抹茶雪糕配方改的
如果是粉料就直接加奶油里






























SELECT * FROM TRBase_06 WHERE CE01='q'
SELECT * FROM TRBase_11 WHERE RelGuid = 'aafc2a9f-9330-462e-9ff8-715ec5076d82'

SELECT * FROM TRBase_15 WHERE CE01='q'
SELECT * FROM TRBase_16 WHERE RelGuid = '5322c95b-ccc0-49ff-9902-3a03a5a56910'


DELETE TRBase_06 WHERE CE01='q'
DELETE TRBase_15 WHERE CE01='q'


DELETE TRBase_11 WHERE RelGuid NOT IN (SELECT RowGuid FROM TRBase_06)
DELETE TRBase_16 WHERE RelGuid NOT IN (SELECT RowGuid FROM TRBase_15)


 string strUserNo = HttpUtility.UrlDecode(string.Format("{0}", Request.Cookies["UserNo"].Value));

            string strGroupName = "";

            ///根据用户编号 获取他是否是管理员
            var userData = new tbUserService().GetEntities(item => item.vUserNo == strUserNo).FirstOrDefault();
            if (userData != null)
            {
                var groupData = new tbGroupService().GetEntities(item => item.RowGuid == userData.GroupRowGuid).FirstOrDefault();
                if (groupData != null)
                {
                    strGroupName = groupData.vGroupName;
                }
            }
            string strBM04 = "";//当前登陆人 所在部门等级
            string strBM05 = "";//
            string strBM06 = "";//当前登陆人 是否是上级
            string strRowID = "";
            ///当前用户单位
            string strOuGuid = HttpUtility.UrlDecode(string.Format("{0}", Request.Cookies["OuGuid"].Value));

            var ouData = new FrameOuService().GetEntities(item => item.RowGuid == strOuGuid).FirstOrDefault();
            if (ouData != null)
            {
                strRowID = ouData.RowID.ToString();
                strBM06 = ouData.BM06; //是否是上级。0,1
                strBM04 = ouData.BM04;
                strBM05 = ouData.BM05;
            }

            string strRowFilter = " 1=1 ";













 if (strGroupName != "系统管理员")
            {
                //根据当前部门等级 0级看全部 

                //如果为上级 则进一位
                if (strBM06 == "1")
                {
                    strBM04 = Convert.ToString(Convert.ToInt16(strBM04) - 1);

                    var oulist = new FrameOuService().GetEntities(p => p.RowGuid == strOuGuid).FirstOrDefault();
                    int iNextId = Convert.ToInt16(oulist.NextID);
                    oulist = new FrameOuService().GetEntities(p => p.RowID == iNextId).FirstOrDefault();

                    strOuGuid = oulist.RowGuid;
                }


                if (strBM04 == "1")
                {
                    strRowFilter += " AND CE08 = '" + strOuGuid + "'";
                }
                if (strBM04 == "2")
                {
                    strRowFilter += " AND CE09 = '" + strOuGuid + "'";
                }
                if (strBM04 == "3")
                {
                    strRowFilter += " AND CE10 = '" + strOuGuid + "'";
                }
                if (strBM04 == "4")
                {
                    strRowFilter += " AND CE11 = '" + strOuGuid + "'";
                }
            }
			
			
			
			
			
			  #region 添加单位等级5个字段数据源

            ///如果是营计划，则单位名称在有多个 的情况下，获取第一个单位名称
            string strCE11 = "";

            if (string.Format("{0}", Request["type"]) == "ying")
            {
                string[] strSplit = Detail_TRBase_06.CE11.Split(',');
                strCE11 = strSplit[0];
            }
            else
            {
                strCE11 = Detail_TRBase_06.CE11;
            }

            string strOunameA = "";
            var listouaA = new NARO.DAL.FrameOu().SelectOUGuid(strCE11);
            if (listouaA.Count > 0)
            {
                strOunameA = listouaA[0]["RowID"].ToString();
             
            }
            string strRowIDItemaA = new NARO.DAL.FrameOu().GetAllSJ(strOunameA);

            string strBM04ItemaA = new NARO.DAL.FrameOu().GetAllBM04(strOunameA);

            string[] strArraA = strRowIDItemaA.Split(',');
            string[] strArraB = strBM04ItemaA.Split(',');
            #endregion

            for (int j = 0; j < strArraA.Length; j++)
            {
                if (strArraB[j].ToString() == "0")
                {
                    Detail_TRBase_06.CE26 = strArraA[j];
                }
                else if (strArraB[j].ToString() == "1")
                {
                    Detail_TRBase_06.CE27 = strArraA[j];
                }
                else if (strArraB[j].ToString() == "2")
                {
                    Detail_TRBase_06.CE28 = strArraA[j];
                }
                else if (strArraB[j].ToString() == "3")
                {
                    Detail_TRBase_06.CE29 = strArraA[j];
                }
                else if (strArraB[j].ToString() == "4")
                {
                    if (string.Format("{0}", Request["type"]) == "ying")
                    {
                        Detail_TRBase_06.CE30 = "";
                    }
                    else
                    {
                        Detail_TRBase_06.CE30 = strArraA[j];
                    }

                }
            }

























（武藏）既然你诚心诚意的发问了， 
（小次郎）我们就大发慈悲的告诉你！ 
（武藏）为了防止世界被破坏， 
（小次郎）为了保护世界的和平； 
（武藏）贯彻爱与真实的邪恶， 
（小次郎）可爱又迷人的反派角色~~ 
（武藏）武藏！ 
（小次郎）小次郎！ 
（武藏）我们是穿梭在银河的火箭队！ 
（小次郎）白洞，白色的明天在等着我们！！ 
（喵喵）就是这样~喵~~~~ 




那个你用醋加苏打粉  泡全水一下午就干净了
