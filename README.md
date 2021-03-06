# WidgetSampleII
# A second widget sample to provide a safe environment to create and test a widget with an extractor
<?xml version="1.0" encoding="UTF-8"?>
<OpenCOBData id="extractorID">
  <ExtractorSpec platform="gmail" language="en">
    <!-- Set up a regexp to match content. -->
    <Search input_type="text">
      <!-- input_fields - a comma-separated list of
       email parts to look in.
       Supported values: from_email, to_email, cc_email, bcc_email,
       date_sent, date_received, subject, body, id, list_id, list_unsubscribe.
       Default: subject,body. -->
      <Pattern input_fields="subject, body, id, list_id, list_unsubscribe">
        <!-- In yourRegularExpression, include one or more named
         sub-patterns in angle brackets which identify substrings that
         can be referred to in @outputSource below.
         The regular expression can also contain ?M=objectType
         to refer to a <DataObject> in the same file. -->
        <![CDATA[(Received-SPF.*client-ip=(.*);)]]>
      </Pattern>
    </Search>
    <!-- Set up the output. -->
    <Response platform="gmail" format="cardgadget">
      <!-- outputSource specifies what to return.
       To return part of the string that matched the expression,
       use a sub-pattern name specified in the <Pattern>.
       To return an entire email field, use a built-in
       variable: __SUBJECT__, __BODY__, __DATE_SENT__,
       __DATE_RECEIVED, __FROM_ADDRESS__, __TO_ADDRESS__,
       __CC_EMAIL__, __BCC_EMAIL__, __MESSAGE_ID__, __LIST_ID__,
       or __LIST_UNSUBSCRIBE__. In this case, you don't need to use
       the <Pattern> tag. -->
      <Output name="outputFieldName">{@outputSource}!</Output>
    </Response>
  </ExtractorSpec>

  <!-- Optional: a list of literal strings to look for. Incorporate this
   into the regular expression above by referring to objectType. -->
  <DataObject id="dataObjectID" type="objectType">
    <QueryName value="literal"/>
    ...
  </DataObject>

  <!-- Repeat to define more string repositories. -->
  <DataObject>...</DataObject>
  ...

</OpenCOBData>
