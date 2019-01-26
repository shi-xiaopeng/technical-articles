i```
UPDATE coupon SET use_count=use_count+1 WHERE id='1234565'
UPDATE coupon SET use_count=IF(use_count>1, 0, use_count-1) 
               WHERE id="174893"

```
