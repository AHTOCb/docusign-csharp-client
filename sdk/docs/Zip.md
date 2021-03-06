# DocuSign.eSign.Model.Zip
## Properties

Name | Type | Description | Notes
------------ | ------------- | ------------- | -------------
**AnchorCaseSensitive** | **string** | When set to **true**, the anchor string does not consider case when matching strings in the document. The default value is **true**. | [optional] 
**AnchorHorizontalAlignment** | **string** | Specifies the alignment of anchor tabs with anchor strings. Possible values are **left** or **right**. The default value is **left**. | [optional] 
**AnchorIgnoreIfNotPresent** | **string** | When set to **true**, this tab is ignored if anchorString is not found in the document. | [optional] 
**AnchorMatchWholeWord** | **string** | When set to **true**, the anchor string in this tab matches whole words only (strings embedded in other strings are ignored.) The default value is **true**. | [optional] 
**AnchorString** | **string** | Anchor text information for a radio button. | [optional] 
**AnchorUnits** | **string** | Specifies units of the X and Y offset. Units could be pixels, millimeters, centimeters, or inches. | [optional] 
**AnchorXOffset** | **string** | Specifies the X axis location of the tab, in achorUnits, relative to the anchorString. | [optional] 
**AnchorYOffset** | **string** | Specifies the Y axis location of the tab, in achorUnits, relative to the anchorString. | [optional] 
**Bold** | **string** | When set to **true**, the information in the tab is bold. | [optional] 
**ConcealValueOnDocument** | **string** | When set to **true**, the field appears normally while the recipient is adding or modifying the information in the field, but the data is not visible (the characters are hidden by asterisks) to any other signer or the sender.  When an envelope is completed the information is available to the sender through the Form Data link in the DocuSign Console.  This setting applies only to text boxes and does not affect list boxes, radio buttons, or check boxes. | [optional] 
**ConditionalParentLabel** | **string** | For conditional fields this is the TabLabel of the parent tab that controls this tab&#39;s visibility. | [optional] 
**ConditionalParentValue** | **string** | For conditional fields, this is the value of the parent tab that controls the tab&#39;s visibility.  If the parent tab is a Checkbox, Radio button, Optional Signature, or Optional Initial use \&quot;on\&quot; as the value to show that the parent tab is active.  | [optional] 
**CustomTabId** | **string** | The DocuSign generated custom tab ID for the custom tab to be applied. This can only be used when adding new tabs for a recipient. When used, the new tab inherits all the custom tab properties. | [optional] 
**DisableAutoSize** | **string** | When set to **true**, disables the auto sizing of single line text boxes in the signing screen when the signer enters data. If disabled users will only be able enter as much data as the text box can hold. By default this is false. This property only affects single line text boxes. | [optional] 
**DocumentId** | **string** | Specifies the document ID number that the tab is placed on. This must refer to an existing Document&#39;s ID attribute. | [optional] 
**ErrorDetails** | [**ErrorDetails**](ErrorDetails.md) |  | [optional] 
**Font** | **string** | The font to be used for the tab value. Supported Fonts: Arial, Arial, ArialNarrow, Calibri, CourierNew, Garamond, Georgia, Helvetica,   LucidaConsole, Tahoma, TimesNewRoman, Trebuchet, Verdana, MSGothic, MSMincho, Default. | [optional] 
**FontColor** | **string** | The font color used for the information in the tab.  Possible values are: Black, BrightBlue, BrightRed, DarkGreen, DarkRed, Gold, Green, NavyBlue, Purple, or White. | [optional] 
**FontSize** | **string** | The font size used for the information in the tab.  Possible values are: Size7, Size8, Size9, Size10, Size11, Size12, Size14, Size16, Size18, Size20, Size22, Size24, Size26, Size28, Size36, Size48, or Size72. | [optional] 
**Italic** | **string** | When set to **true**, the information in the tab is italic. | [optional] 
**Locked** | **string** | When set to **true**, the signer cannot change the data of the custom tab. | [optional] 
**MaxLength** | **int?** | An optional value that describes the maximum length of the property when the property is a string. | [optional] 
**MergeField** | [**MergeField**](MergeField.md) |  | [optional] 
**Name** | **string** |  | [optional] 
**OriginalValue** | **string** | The initial value of the tab when it was sent to the recipient.  | [optional] 
**PageNumber** | **string** | Specifies the page number on which the tab is located. | [optional] 
**RecipientId** | **string** | Unique for the recipient. It is used by the tab element to indicate which recipient is to sign the Document. | [optional] 
**RequireAll** | **string** | When set to **true** and shared is true, information must be entered in this field to complete the envelope.  | [optional] 
**Required** | **string** | When set to **true**, the signer is required to fill out this tab | [optional] 
**RequireInitialOnSharedChange** | **string** | Optional element for field markup. When set to **true**, the signer is required to initial when they modify a shared field. | [optional] 
**SenderRequired** | **string** | When set to **true**, the sender must populate the tab before an envelope can be sent using the template.   This value tab can only be changed by modifying (PUT) the template.   Tabs with a &#x60;senderRequired&#x60; value of true cannot be deleted from an envelope. | [optional] 
**Shared** | **string** | When set to **true**, this custom tab is shared. | [optional] 
**Status** | **string** | Indicates the envelope status. Valid values are:  * sent - The envelope is sent to the recipients.  * created - The envelope is saved as a draft and can be modified and sent later. | [optional] 
**TabId** | **string** | The unique identifier for the tab. The tabid can be retrieved with the [ML:GET call].      | [optional] 
**TabLabel** | **string** | The label string associated with the tab. | [optional] 
**TabOrder** | **string** |  | [optional] 
**TemplateLocked** | **string** | When set to **true**, the sender cannot change any attributes of the recipient. Used only when working with template recipients.  | [optional] 
**TemplateRequired** | **string** | When set to **true**, the sender may not remove the recipient. Used only when working with template recipients. | [optional] 
**Underline** | **string** | When set to **true**, the information in the tab is underlined. | [optional] 
**UseDash4** | **string** |  | [optional] 
**ValidationMessage** | **string** | The message displayed if the custom tab fails input validation (either custom of embedded). | [optional] 
**ValidationPattern** | **string** | A regular expressionn used to validate input for the tab. | [optional] 
**Value** | **string** | Specifies the value of the tab.  | [optional] 
**Width** | **int?** | Width of the tab in pixels. | [optional] 
**XPosition** | **string** | This indicates the horizontal offset of the object on the page. DocuSign uses 72 DPI when determining position. | [optional] 
**YPosition** | **string** | This indicates the vertical offset of the object on the page. DocuSign uses 72 DPI when determining position. | [optional] 

[[Back to Model list]](../README.md#documentation-for-models) [[Back to API list]](../README.md#documentation-for-api-endpoints) [[Back to README]](../README.md)

