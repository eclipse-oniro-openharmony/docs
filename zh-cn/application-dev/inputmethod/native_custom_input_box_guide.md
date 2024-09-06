# �Ի�༭�򿪷�ָ�� (C/C++)


## ��������

IME Kit֧�ֿ�����ʹ���Ի���������Զ���༭�������뷨Ӧ�ý�����������ʾ���������뷨�������������뷨Ӧ�õ��ı��༭����֪ͨ�ȣ����ĵ����ܿ��������ʹ��C/C++��ɴ˹��ܿ�����

## �ӿ�˵��

��ϸ�ӿ�˵����ο�[InputMethod�ӿ��ĵ�](../reference/apis-ime-kit/_input_method.md)��

## ��Ӷ�̬���ӿ�

CMakeLists.txt���������lib��

```txt
libohinputmethod.z.so
```

## ����ͷ�ļ�

```c
#include <inputmethod/inputmethod_controller_capi.h>
```


## �����뷨

��������Ҫ��������ʱ��ͨ�����ýӿ�[OH_InputMethodController_Attach](../reference/apis-ime-kit/_input_method.md#oh_inputmethodcontroller_attach)�����뷨���󶨳ɹ����û�����ͨ�����뷨�������֡�

1. ����InputMethod_TextEditorProxyʵ����ʾ������������ʾ��

   ```c
   // ����InputMethod_TextEditorProxyʵ��
   InputMethod_TextEditorProxy *textEditorProxy = OH_TextEditorProxy_Create();
   ```
   
3. ����InputMethod_AttachOptionsʵ�������ð����뷨ʱ��ѡ�ʾ������������ʾ��

   ```c
   // ����InputMethod_AttachOptionsʵ����ѡ��showKeyboard����ָ���˴ΰ󶨳ɹ����Ƿ���ʾ���̣��˴���Ŀ����ʾ����Ϊ��
   bool showKeyboard = true;
   InputMethod_AttachOptions *options = OH_AttachOptions_Create(showKeyboard);
   ```

4. ����OH_InputMethodController_Attach��������뷨���񣬵��óɹ��󣬿��Ի�ȡ�����ں����뷨������InputMethod_InputMethodProxy��ʾ������������ʾ��

   ```c
   InputMethod_InputMethodProxy *inputMethodProxy = nullptr;
   // ���������
   if (OH_InputMethodController_Attach(textEditorProxy, options, &inputMethodProxy) != InputMethod_ErrorCode::IME_ERR_OK) {
       OH_LOG_Print(LOG_APP, LOG_ERROR, 0, "testTag", "Attach failed!");
   }
   ```

## ��ʾ/������幦��

�󶨳ɹ��󣬿���ʹ�û�ȡ����[InputMethod_InputMethodProxy](../reference/apis-ime-kit/_input_method.md#inputmethod_inputmethodproxy)���������뷨������Ϣ��ʾ������������ʾ��

```c
// ��ʾ����
if (OH_InputMethodProxy_ShowKeyboard(inputMethodProxy) != InputMethod_ErrorCode::IME_ERR_OK) {
    OH_LOG_Print(LOG_APP, LOG_ERROR, 0, "testTag", "ShowKeyboard failed!");
}
// ���ؼ���
if (OH_InputMethodProxy_HideKeyboard(inputMethodProxy) != InputMethod_ErrorCode::IME_ERR_OK) {
    OH_LOG_Print(LOG_APP, LOG_ERROR, 0, "testTag", "HideKeyboard failed!");
}
// ֪ͨ�����������Ϣ�仯
if (OH_InputMethodProxy_NotifyConfigurationChange(inputMethodProxy, InputMethod_EnterKeyType::IME_ENTER_KEY_GO, InputMethod_TextInputType::IME_TEXT_INPUT_TYPE_TEXT) != InputMethod_ErrorCode::IME_ERR_OK) {
    OH_LOG_Print(LOG_APP, LOG_ERROR, 0, "testTag", "NotifyConfigurationChange failed!");
}
```

## �������뷨Ӧ�õ�����/֪ͨ

1. ��Ҫ��ʵ�ֶ����뷨Ӧ�÷��͵������֪ͨ����Ӧ��������ʾ������������ʾ��

   ```c
   // ʵ��InputMethod_TextEditorProxy�е����뷨Ӧ���¼���Ӧ����
   void GetTextConfig(InputMethod_TextEditorProxy *textEditorProxy, InputMethod_TextConfig *config)
   {
       // �������뷨���͵Ļ�ȡ�������������
   }
   void InsertText(InputMethod_TextEditorProxy *textEditorProxy, const char16_t *text, size_t length)
   {
       // �������뷨���͵Ĳ����ı�����
   }
   void DeleteForward(InputMethod_TextEditorProxy *textEditorProxy, int32_t length)
   {
       // �������뷨���͵�ɾ���ı�����
   }
   // ......
   ```

2. ��ʵ�ֺ����Ӧ���������õ�[InputMethod_TextEditorProxy](../reference/apis-ime-kit/_input_method.md#inputmethod_texteditorproxy)�У���ͨ�������뷨ʱ���õ�[OH_InputMethodController_Attach](../reference/apis-ime-kit/_input_method.md#oh_inputmethodcontroller_attach)�������õ����뷨����У���ɼ���ע�ᡣʾ������������ʾ

   ```c
   // ��ʵ�ֺõ���Ӧ���������õ�InputMethod_TextEditorProxy��
   OH_TextEditorProxy_SetGetTextConfigFunc(textEditorProxy, GetTextConfig);
   OH_TextEditorProxy_SetInsertTextFunc(textEditorProxy, InsertText);
   OH_TextEditorProxy_SetDeleteForwardFunc(textEditorProxy, DeleteForward);
   ```

## ������뷨

���༭��ʧ������Ҫ����ʹ�����뷨��ͨ���ӿ�[OH_InputMethodController_Detach](../reference/apis-ime-kit/_input_method.md#oh_inputmethodcontroller_detach)�����뷨��ܽ��

```c
// ����������
if (OH_InputMethodController_Detach(inputMethodProxy) != InputMethod_ErrorCode::IME_ERR_OK) {
    OH_LOG_Print(LOG_APP, LOG_ERROR, 0, "testTag", "Detach failed!");
}
inputMethodProxy = nullptr;
OH_TextEditorProxy_Destroy(textEditorProxy);
textEditorProxy = nullptr;
OH_AttachOptions_Destroy(options);
options = nullptr;
```

