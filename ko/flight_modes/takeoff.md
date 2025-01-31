# 이륙 모드

[<img src="../../assets/site/position_fixed.svg" title="Position fix required (e.g. GPS)" width="30px" />](../getting_started/flight_modes.md#key_position_fixed)

* 이륙 (Takeo) </ 0> 비행 모드는 기체가 지정된 높이로 떨어져 나가고 추가 입력을 기다립니다.</p> 

> **Note** * This mode requires GPS. * This mode is automatic (RC control is disabled [by default](../advanced_config/parameter_reference.md#COM_RC_OVERRIDE) except to change modes). * The vehicle must be armed before this mode can be engaged.

The specific behaviour for each vehicle type is described below.

## 멀티 헬기 (MC)

멀티 로터는  MIS_TAKEOFF_ALT </ 0>에 정의 된 고도까지 상승하고 위치를 유지합니다.</p>

<p>이륙은 다음 매개 변수의 영향을받습니다.</p>

<table>
<thead>
<tr>
  <th>Parameter</th>
  <th>Description</th>
</tr>
</thead>
<tbody>
<tr>
  <td><a href="../advanced_config/parameter_reference.md#MIS_TAKEOFF_ALT">MIS_TAKEOFF_ALT
</a></td>
  <td>이륙 중 목표 고도 (기본값 : 2.5m)</td>
</tr>
<tr>
  <td><a href="../advanced_config/parameter_reference.md#MPC_TKO_SPEED">MPC_TKO_SPEED
</a></td>
  <td>상승 속도 (기본값 : 1.5m / s)</td>
</tr>
</tbody>
</table>

<h2 id="fixed_wing">Fixed Wing (FW)</h2>

<p>항공기는 <em> 투석기 / 발사 모드 </ 0> 또는 <em> 활주로 이륙 모드 </ 0>를 사용하여 현재 방향으로 이륙합니다. 모드는 기본적으로 투석기 / 손발기가되지만, <code> RWTO_TKOFF </ 0>를 사용하여 활주로 이륙으로 설정할 수 있습니다.</p>

<p><em> 투석기 / 손 발사 모드 </ 0>에서 기체는 최대 스로틀 상승 (약 2 초 내에 <code> RWTO_MAX_THR </ 1>까지 상승)을 수행합니다. 고도 오류 <<a href="#FW_CLMBOUT_DIFF"> FW_CLMBOUT_DIFF </ 0>가되면 일반 탐색이 진행됩니다.</p>

<blockquote>
  <p><strong> 참고 </ 0> 위에 논의 된 동작 외에도 일부 조건이 충족 될 때까지 시작 시퀀스가 ​​시작되지 않도록 차단하는 시작 탐지기가 있습니다. 투석기 발사의 경우 이는 약간의 가속 임계 값입니다.</p>
</blockquote>

<p><em> 활주로 이륙 모드 </ 0>의 위상은 다음과 같습니다.</p>

<ol start="1">
<li><strong> 스로틀 램프 </ 0> : 이륙을위한 최소 속도 (<a href="#FW_AIRSPD_MIN"> FW_AIRSPD_MIN </ 1> x <a href="#RWTO_AIRSPD_SCL"> RWTO_AIRSPD_SCL </ 2>)에 도달 할 때까지 활주로에 고정 (피치 고정, ) </li>
<li><strong> 이륙 </ 0> : 피치를 높이고 기체 고도> 항법 고도 (<a href="#RWTO_NAV_ALT"> RWTO_NAV_ALT </ 1>)까지 계속하십시오.</li>
<li>



<strong> 등산 </ 0> :지면 위의 고도 <a href="#FW_CLMBOUT_DIFF"> FW_CLMBOUT_DIFF </ 1>까지 상승하십시오.
 이 단계에서는 롤 및 제목 제한이 제거됩니다.</li>
</ol>

<p>Takeoff is affected by the following parameters:</p>

<table>
<thead>
<tr>
  <th>Parameter</th>
  <th>Description</th>
</tr>
</thead>
<tbody>
<tr>
  <td><span id="RWTO_TKOFF"></span><a href="../advanced_config/parameter_reference.md#RWTO_TKOFF">RWTO_TKOFF</a>
</td>
  <td>랜딩 기어가있는 활주로 이륙. 기본값 : 비활성화 됨</td>
</tr>
<tr>
  <td><span id="RWTO_MAX_THR"></span><a href="../advanced_config/parameter_reference.md#RWTO_MAX_THR">RWTO_MAX_THR</a>
</td>
  <td>활주로 이륙 중 최대 스로틀.</td>
</tr>
<tr>
  <td><span id="FW_CLMBOUT_DIFF"></span><a href="../advanced_config/parameter_reference.md#FW_CLMBOUT_DIFF">FW_CLMBOUT_DIFF</a>
</td>
  <td>등반 고도 차이.</td>
</tr>
<tr>
  <td><span id="FW_AIRSPD_MIN"></span><a href="../advanced_config/parameter_reference.md#FW_AIRSPD_MIN">FW_AIRSPD_MIN</a></td>
  <td>Minimum Airspeed (최소 속도). TECS 컨트롤러가 대기 속도를보다 적극적으로 높이려고 시도합니다.</td>
</tr>
<tr>
  <td><span id="RWTO_AIRSPD_SCL"></span><a href="../advanced_config/parameter_reference.md#RWTO_AIRSPD_SCL">RWTO_AIRSPD_SCL</a>
</td>
  <td>최소 이륙을위한 속도의 스케일링 계수. 피치는 대기 속도에 도달하면 증가합니다 : <code> FW_AIRSPD_MIN </ 0> * <code> RWTO_AIRSPD_SCL </ 0></td>
</tr>
<tr>
  <td><span id="RWTO_NAV_ALT"></span><a href="../advanced_config/parameter_reference.md#RWTO_NAV_ALT">RWTO_NAV_ALT</a>
</td>
  <td>지면 위의 고도 (AGL). 약간의 굴림을 허용하는 충분한 지상고가 있습니다. <code> RWTO_NAV_ALT </ 0>에 도달 할 때까지 비행기는 수평을 유지하고 표제를 지키기 위해 방향타 만 사용됩니다 (<span id="RWTO_HDG"> <a href="../advanced_config/parameter_reference.md#RWTO_HDG"> RWTO_HDG </ 2> 참조). <code> FW_CLMBOUT_DIFF </ 0>> 0이면 <code> FW_CLMBOUT_DIFF </ 0> 아래에 있어야합니다.</td>
</tr>
</tbody>
</table>

<blockquote>
  <p>



<strong> 참고 </ 0> 기체는 항상 이륙 중에 (<a href="../advanced_config/parameter_reference.md#FW_THR_MIN"> FW_THR_MIN </ 1>, <a href="../advanced_config/parameter_reference.md#FW_THR_MAX"> FW_THR_MAX </ 2>) 정상 FW 최대 / 최소 스로틀 설정을 준수합니다.
</p>
</blockquote>

<h2>VTOL</h2>

<p>A VTOL follows the TAKEOFF behavior and parameters of <a href="#fixed_wing">Fixed Wing</a> when in FW mode, and of <a href="#multi-copter-mc">Multicopter</a> when in MC mode.</p>

<!-- this maps to AUTO_TAKEOFF in dev -->