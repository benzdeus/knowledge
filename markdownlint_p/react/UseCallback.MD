# useCallback

useCallback คือการ Cache Function ไม่ ถูกเรียกครั้งแรกเมื่อมีการ Render โดยจะถูกเรียกก็ต่อเมื่อสั่ง Call ฟังก์ชัน และ ค่าใน Array deps มีการเปลี่ยนแปลง โดย Return ออกเป็น Function

## หลักการของ useCallback คือการ Cache ฟังก์ชันไว้

- ไม่ ถูกเรียกเมื่อมีการ Render (จะถูกเรียกเมื่อเราสั่ง Call ฟังก์ชันเอง)
- ถูกเรียกอีกครั้งเมื่อสั่ง Call ฟังก์ชัน และ ค่าใน Array deps มีการเปลี่ยนแปลง
- Return ออกเป็น Function

## Note
useCallback(fn, deps) จะเท่ากับ useMemo(() => fn, deps)