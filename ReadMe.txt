




































sys
orcl




mstsc /admin /v:Ŀ��ip



192.168.0.211   
218.2.135.1                    

 ������250�ˣ�ţ��250�ˣ�����35�ˣ���20�ˣ���ݼ�����֮һ����ȫ��1��������4��

ȫ���͵��ƻ�Ͼ��ȣ��������ϻ�Ϻ���ȵ���ȫ���ڻ����ŵ�΢�µ�����Һ���Ͼ��ȣ���ɸ����
Ȼ�󵹽����������ˮԡ����140�ȿ�20��30���ӣ�������������������Ϳ�����



http://www.open-open.com/lib/view/open1354515766351.html


������ 08:36:03
http://newb2c.coseo.cn/admin/login.aspx


http://localhost/zzgz/Content/css/bootstrap.min14ed.css?v=3.3.6



˫��  ��ͨ����980  ��������1350 .�˶��������2480 �۲�ר�ÿ���780 


http://www.cnblogs.com/artwl/archive/2012/03/31/2427019.html






�䷽�ܼ�
����3����������250ML����ϲ��������ˮ��150�˵�200��
ϸɰ��40��



����+�ǣ�����40����ˮ�򷢳�˿��״�������ٰ���ˮ���ȵ�80�ȣ��ٴ�һ�ᣬ��һ�㲻���ڼ���
Ȼ�����ʹ�6�ַ����ң�Ũ����
�����ô������
Ȼ�󼱶��Ϳ�����
�������Ĩ��ѩ���䷽�ĵ�
����Ƿ��Ͼ�ֱ�Ӽ�������






























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

            ///�����û���� ��ȡ���Ƿ��ǹ���Ա
            var userData = new tbUserService().GetEntities(item => item.vUserNo == strUserNo).FirstOrDefault();
            if (userData != null)
            {
                var groupData = new tbGroupService().GetEntities(item => item.RowGuid == userData.GroupRowGuid).FirstOrDefault();
                if (groupData != null)
                {
                    strGroupName = groupData.vGroupName;
                }
            }
            string strBM04 = "";//��ǰ��½�� ���ڲ��ŵȼ�
            string strBM05 = "";//
            string strBM06 = "";//��ǰ��½�� �Ƿ����ϼ�
            string strRowID = "";
            ///��ǰ�û���λ
            string strOuGuid = HttpUtility.UrlDecode(string.Format("{0}", Request.Cookies["OuGuid"].Value));

            var ouData = new FrameOuService().GetEntities(item => item.RowGuid == strOuGuid).FirstOrDefault();
            if (ouData != null)
            {
                strRowID = ouData.RowID.ToString();
                strBM06 = ouData.BM06; //�Ƿ����ϼ���0,1
                strBM04 = ouData.BM04;
                strBM05 = ouData.BM05;
            }

            string strRowFilter = " 1=1 ";













 if (strGroupName != "ϵͳ����Ա")
            {
                //���ݵ�ǰ���ŵȼ� 0����ȫ�� 

                //���Ϊ�ϼ� ���һλ
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
			
			
			
			
			
			  #region ��ӵ�λ�ȼ�5���ֶ�����Դ

            ///�����Ӫ�ƻ�����λ�������ж�� ������£���ȡ��һ����λ����
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

























����أ���Ȼ����ĳ���ķ����ˣ� 
��С���ɣ����Ǿʹ󷢴ȱ��ĸ����㣡 
����أ�Ϊ�˷�ֹ���类�ƻ��� 
��С���ɣ�Ϊ�˱�������ĺ�ƽ�� 
����أ��᳹������ʵ��а�� 
��С���ɣ��ɰ������˵ķ��ɽ�ɫ~~ 
����أ���أ� 
��С���ɣ�С���ɣ� 
����أ������Ǵ��������ӵĻ���ӣ� 
��С���ɣ��׶�����ɫ�������ڵ������ǣ��� 
����������������~��~~~~ 




�Ǹ����ô׼��մ��  ��ȫˮһ����͸ɾ���
