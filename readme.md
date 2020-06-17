## 简单的多项选择对话框
```
    api 'com.seeker.tool:datetime-picker:0.0.3'
```
- 多选选择框
- 日期选择框

![截图](/screen.png)

```java
          if (mDatePicker == null) {
                mDatePicker = new TextPickerDialogUtil(this);
                mDatePicker.addItems(getItem(101, "", " 年", DateManager.MIN_YEAR), 1f, true);
                mDatePicker.addItems(getItem(12, "", "月", 1), 1f, false);
                mDatePicker.setListener(new TextPickerDialogUtil.OnSelectChangeListener() {
                    @Override
                    public void onDateChange(Integer[] value, NumberPicker changePicker) {
                    }

                    @Override
                    public void onConfirm(Integer[] value) {
                        int year = value[0] + DateManager.MIN_YEAR;
                        int month = value[1];
                        setTitleString(year, month);
                        String day = "1";
                        if (mCalendarLayout != null) {
                            day = mCalendarLayout.getChooseDay();
                        }
                        Calendar calendar = Calendar.getInstance(Locale.CHINA);
                        if (DateUtils.isValidDate(String.valueOf(year + "-" + (month + 1) + "-" + day))) {
                            calendar.set(year, month, Util.parseInt(day), 0, 0);
                        } else {
                            calendar.set(year, month, 1, 0, 0);
                        }

                        mCalendarLayout.setCurrentDate(calendar);
                    }
                });

//            }
            mDatePicker.pickers.get(0).setValue(calendar.get(Calendar.YEAR) - DateManager.MIN_YEAR);
            mDatePicker.pickers.get(1).setValue(calendar.get(Calendar.MONTH));
            mDatePicker.show("选择要跳转的年月");
```
