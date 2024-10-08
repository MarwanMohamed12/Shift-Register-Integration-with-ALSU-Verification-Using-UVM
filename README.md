# Shift-Register-Integration-with-ALSU-Verification-Using-UVM

1. Objective

To integrate a shift register into the Arithmetic Logic Shift Unit (ALSU) and verify the combined design using two distinct UVM environments: one for the ALSU and another for the shift register. The ALSU will be an active agent driving the interface, while the shift register will be passive, only monitoring its interface.
2. Design Details

    ALSU: Performs arithmetic, logical, and shift operations.
    Shift Register: Executes shift and rotate operations.
    The shift register will now be part of the ALSU design and connected as follows:
        Data Connections:
            The datain port of the shift register is connected to the out port of the ALSU.
            The dataout port of the shift register is connected to a new 6-bit bus, out_shift_reg.
            The out_shift_reg value is assigned to the ALSU out port during shift and rotate operations.

3. Testbench Architecture

    ALSU Environment: Active, driving the interface of the ALSU.
    Shift Register Environment: Passive, monitoring the shift register interface.
    Virtual Interface: Shared between the two environments using UVM configuration.
    Configurations: Two configuration objects are created:
        ALSU Config: Set as UVM_ACTIVE to drive the ALSU interface.
        Shift Register Config: Set as UVM_PASSIVE, monitoring the shift register interface and sending data to its scoreboard and coverage collector.

4. UVM Steps

    Top Module:
        Add the ALSU and shift register interfaces.
        Use assign statements to connect the interfaces, e.g., assign shift_if.serial_in = alsu_if.serial_in;.
    Config DB:
        Pass both interfaces through the UVM configuration database (config_db).
    Agent Behavior:
        In the build phase of the agents, check the is_active variable:
            If UVM_ACTIVE, build the driver and sequencer.
        In the connect phase, connect the driver, sequencer, and virtual interface if the agent is active.

5. Verification and Coverage

    Functional, code, and assertion coverage is collected for both ALSU and the shift register.
    The shift register environment is responsible for collecting coverage and checking data validity through its scoreboard.

6. Assertions

Assertions are added to the ALSU and shift register to check the correct behavior of output flags and internal states. These assertions are guarded by conditional compilation using SIM.
Deliverables

    Code and Simulation:
        Screenshots of the top module, UVM files, ALSU, and shift register design.
        Coverage reports: functional, code, and assertion coverage.

    Final Documentation:
        A detailed report including screenshots of waveforms showing input driving.
        Coverage reports and verification plan.

This setup ensures a clear separation between the active and passive agents, allowing thorough verification of both the ALSU and the shift register.
