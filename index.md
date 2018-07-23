#ODS层数据合并任务修改建议

1. s_ebsdb_wsh_wsh_new_deliveries任务

    * 不使用max_pt('dp_ods.s_ebsdb_cux_xx_wsh_new_deliveries_log')
    
    ```text
     LEFT JOIN (
          SELECT DELIVERY_ID
          FROM dp_ods.s_ebsdb_cux_xx_wsh_new_deliveries_log
          WHERE action = 'DELETE' AND ds = max_pt('dp_ods.s_ebsdb_cux_xx_wsh_new_deliveries_log'))
        del_log ON concat(del_log.DELIVERY_ID) = concat(L1.DELIVERY_ID);
    ```
    - ds不使用in查询
    ```text
    FROM dp_ods.s_ebsdb_wsh_wsh_new_deliveries_delta_hh
    WHERE ds IN (20180720) AND hhmm IN ('1145', '2345')
    ```
    - 去除不必要的连接函数 concat
    ```text
    ON concat(del_log.DELIVERY_ID) = concat(L1.DELIVERY_ID)
    ```
2. s_biio_dbo_crm_spor_budget_sync_cnrate任务
    
    - 没有找到该任务，请在运维中心将周期性失败实例置成功
    
3. s_eap_dbo_ap_estimation_delta 任务
    
    - 没有找到该任务，请在运维中心将周期性失败实例置成功



[./second.md]
