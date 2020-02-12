Hi Mr Y,
Below is the flow which catches two exceptions.
1- java.net.connectException
2- java.io.IOException

    <flow name="testpocFlow">
        <file:inbound-endpoint path="C:\Users\zubair.rafaqat\Desktop\test\in\1111" responseTimeout="10000" doc:name="File">
            <file:filename-regex-filter pattern="file:filename-regex-filter caseSensitive=false, pattern=.*xml" caseSensitive="true"/>
        </file:inbound-endpoint>
        <logger level="INFO" doc:name="Logger" message="Flow Logic Here"/>
        <file:outbound-endpoint path="C:\Users\zubair.rafaqat\Desktop\test\out" responseTimeout="10000" doc:name="File">
            <idempotent-redelivery-policy/>
        </file:outbound-endpoint>
        <choice-exception-strategy doc:name="Choice Exception Strategy">
            <catch-exception-strategy when="java.net.connectException" doc:name="java.net.connectException">
                <logger message="Handling Error Related to Connection" level="INFO" doc:name="Logger"/>
            </catch-exception-strategy>
            <catch-exception-strategy when="java.io.IOException" doc:name="java.io.IOException">
                <logger message="Handling Error Related to IO Exception" level="INFO" doc:name="Logger"/>
            </catch-exception-strategy>
        </choice-exception-strategy>
       
    </flow>
