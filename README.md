# 3D Printed Compliant Actuator
(Also Referred to as *THE SHACTUATOR* in various remote regions of the world)

A compact, high-performance open-source actuator for advanced robotics, designed and built to explore fundamental principles of electronics, motors, and gearboxes for applications like robotic locomotion.

**[EMBED VIDEO/GIF OF ACTUATOR IN ACTION HERE]**

---

## Table of Contents
* [Introduction](#introduction)
* [Project Goals & Requirements](#project-goals--requirements)
* [Design Philosophy: Gearbox Selection](#design-philosophy-gearbox-selection)
    * [Gear Ratio Calculation](#gear-ratio-calculation)
* [Core Components & Bill of Materials](#core-components--bill-of-materials)
* [Mechanical Design & CAD](#mechanical-design--cad)
    * [Overall Assembly](#overall-assembly)
    * [Key Subassemblies](#key-subassemblies)
    * [Design Notes](#design-notes)
* [Manufacturing & 3D Printing Notes](#manufacturing--3d-printing-notes)
* [Assembly](#assembly)
* [Electronics & Control Setup](#electronics--control-setup)
    * [ODrive Tuning](#odrive-tuning)
* [Testing & Performance](#testing--performance)
    * [Max Torque Test](#max-torque-test)
    * [Compliance & Backdrivability](#compliance--backdrivability)
    * [Speed Tests](#speed-tests)
    * [Continuous Torque Test](#continuous-torque-test)
    * [Backlash Evaluation](#backlash-evaluation)
* [Challenges & Lessons Learned](#challenges--lessons-learned)
    * [Power Supply Limitations](#power-supply-limitations)
    * [Material Strain](#material-strain)
* [Future Improvements](#future-improvements)
* [CAD Models](#cad-models)

---

## Introduction

This project explores the design and fabrication of a custom, high-torque-density actuator, dubbed the "SHACTUATOR," leveraging 3D printing and advanced brushless DC motor control. Our primary motivation was the ambitious goal of building a robotic dog, which naturally led us to design and construct our own actuators to deepen our understanding of electronics, motors, and gearboxes. By getting our hands dirty with these foundational elements of applied robotics, we aimed to gain a comprehensive understanding of the root components essential for millions of applications.

## Project Goals & Requirements

The development of the SHACTUATOR was guided by several key objectives:
* **High Torque Density:** Design an actuator capable of delivering substantial torque relative to its size.
* **Compliance & Backdrivability:** Ensure the actuator can yield to external forces and be backdriven, a critical feature for safe and dynamic robotic interaction.
* **3D Print Feasibility:** Leverage FDM 3D printing for rapid prototyping and cost-effectiveness in manufacturing components.
* **Cost-Effectiveness:** Utilize readily available and affordable components where possible.
* **Learning Objectives:** Provide a robust platform for learning about BLDC motor control, gearbox design, and mechatronic system integration.
* **Robotic Dog Application:** Design with the specific requirements of a quadruped robot joint in mind.

## Design Philosophy: Gearbox Selection

When embarking on the design of a custom actuator, selecting the appropriate gearbox type is paramount. We considered three primary options: Planetary, Cycloidal, and Harmonic drives, each with its unique trade-offs in terms of performance, complexity, and manufacturability. To justify our decision, a quick comparative analysis was conducted.

| Criterion              | Harmonic                               | Planetary                          | Cycloidal                          | Notes                                           |
| :--------------------- | :------------------------------------- | :--------------------------------- | :--------------------------------- | :---------------------------------------------- |
| Backlash               | 3                                      | 4                                  | 5 (Excellent)                      |                                                 |
| Torque Density         | 5 (Excellent)                          | 4                                  | 3                                  |                                                 |
| Efficiency             | 4                                      | 2                                  | 5 (Excellent)                      | 5 H will have significant friction if printed   |
| Shock Load Capacity    | 2                                      | 4                                  | 5 (Excellent)                      | 5 H can fail if heavily shocked: Not good for Dog|
| Design Complexity      | 2                                      | 5 (Excellent)                      | 1                                  |                                                 |
| 3D Print Feasibility   | 3                                      | 5 (Excellent)                      | 1                                  |                                                 |
| **Rating (Average)** | **3.17** | **4.00** | **3.33** |                                                 |

*Note: For the above table, a rating of 5 signifies an excellent performance or characteristic for that criterion.*

We ultimately opted for a **Planetary gearbox system**. While Cycloidal and Harmonic drives offer superior efficiency and backlash characteristics, their increased design and printing complexity presented a significant hurdle for a proof-of-concept project. Our primary goal was to validate the overall actuator concept rather than delve into the intricacies of perfecting highly complex 3D-printed cycloidal or harmonic drives. Planetary gearboxes strike a favorable balance, offering sufficient efficiency and ease of fabrication, which was crucial for rapid prototyping.

### Gear Ratio Calculation

Our planetary gearbox was meticulously designed to achieve an **8:1 gear ratio**, effectively multiplying the motor's output torque by eight. We chose helical gears over spur gears for this design. Helical gears provide a smoother and quieter operation due to the gradual engagement of teeth, and more importantly, they offer a higher load capacity by distributing the load across multiple teeth simultaneously. This was a critical consideration given the use of PLA for printed components, as it adds a valuable safety factor by spreading the load and mitigating potential stress concentrations.

<p align="center">
  <img src="images/GEAR_RATIO_CALC.JPEG" alt="Gear Box Calculation" width="600">
  <br>
  <em>Figure 1: Detailed calculations for the 8:1 helical planetary gearbox ratio and teeth selection, ensuring proper meshing and desired reduction.</em>
</p>

## Core Components & Bill of Materials

The SHACTUATOR integrates a select set of components, chosen for their performance, availability, and suitability for the project's goals. The full Bill of Materials (BOM) is detailed below, including component names, quantities, costs, and sourcing information.

* **Encoder Magnet** (Count: 1): Sourced from [DigiKey](https://www.digikey.com/en/products/detail/radial-magnets-inc/9049/6030786).
* **EaglePower 8308 KV90 Brushless Motor** (Count: 1): Designed for agricultural drones, this motor was selected for its low profile, relatively high performance, and competitive price ($69.09 from AliExpress).
    * **Specifications:** Size: 3.62” Dia, 1.12” height; 0.741 lbs; Max Continuous Current 22A; 20 pole pairs.
* **ODrive S1 Controller** (Count: 1): The brain of the operation, this advanced motor controller is essential for precise BLDC motor commutation and control ($169.73 from [ODrive Robotics](https://shop.odriverobotics.com/products/odrive-s1)).
* **OD 95mm ball bearing** (Count: 1): $15.79 from Ucxcell.
* **4-40 Keenserts** (Count: 30): $10.99 from Amazon.
* **M5x30 (h7) steel dowel pin** (Count: 1 pack (3)): $11.89 from Amazon/Misumi.
* **625ZZ bearing** (Count: 1 pack (3)): $5.99 from Ucxcell.
* **M2.5x4 hex cap screw** (Count: 4)
* **#4-40 Flat Head Screw** (various lengths): 1/2" (23 count), 1 1/8" (3 count), 5/8" (4 count).

**Total Project Cost (Components): $282.49**

<p align="center">
  <img src="images/image_5c3504.png" alt="Bill of Materials" width="800">
  <br>
  <em>Figure 2: Detailed Bill of Materials (BOM) including component names, quantities, costs, and sourcing information.</em>
</p>

## Mechanical Design & CAD

The SHACTUATOR's mechanical design emphasizes modularity, enabling ease of assembly, maintenance, and potential future modifications. The entire actuator is ingeniously composed of four main assemblies, meticulously designed to slip together. This modular approach significantly streamlines the construction process and offers flexibility for iterating on specific components.

<p align="center">
  <img src="images/SHACTUATOR_EXPL.jpg" alt="SHACTUATOR Exploded View" width="700">
  <br>
  <em>Figure 3: An exploded view of the SHACTUATOR, illustrating its main components and their arrangement.</em>
</p>

<p align="center">
  <img src="images/SHACTUATOR_ASSY.jpg" alt="SHACTUATOR Assembled View" width="700">
  <br>
  <em>Figure 4: The fully assembled SHACTUATOR, showcasing its compact form factor and integrated design.</em>
</p>

### Overall Assembly

The SHACTUATOR consists of 4 main assemblies that slip together for streamlined integration and maintenance.

### Key Subassemblies

* **End Effector and Bearing:** This assembly forms the primary output of the actuator. Designed with various end effector versions, it facilitates rapid testing and minimizes potential sources of error. The default design allows for direct mounting of these end effectors.
    <p align="center">
      <img src="images/BEARING_ASSY.jpg" alt="Bearing Subassembly" width="600">
      <br>
      <em>Figure 5: Exploded view of the Bearing Subassembly, highlighting the 75mm ID, 90mm OD bearing that supports the actuator's output shaft.</em>
    </p>

* **Actuator Housing:** This critical component serves a dual purpose: it functions as the stationary **ring gear** for the planetary system and acts as a protective shroud for the entire internal assembly. Integrated holes provide passive cooling to dissipate heat generated during operation.
    <p align="center">
      <img src="images/HOUSING.jpg" alt="Housing Component" width="600">
      <br>
      <em>Figure 6: The Housing component, which functions as the ring gear and actuator shroud, showing its internal helical gear teeth and integrated cooling provisions.</em>
    </p>

* **Planetary Carriers:** This subassembly houses the planet gears. It incorporates steel dowel pins and small roller bearings alongside the gears, ensuring smooth and efficient power transmission. A key manufacturing note for this part is the requirement to pause the 3D print mid-way to insert these bearings.
    <p align="center">
      <img src="images/CARRIER_ASSY.jpg" alt="Planet Carrier Subassembly" width="600">
      <br>
      <em>Figure 7: The Planet Carrier Subassembly, showing the arrangement of planet gears, 3x M5 dowel pins, and 3x 5mm ID, 16mm OD bearings, crucial for smooth planetary motion.</em>
    </p>

* **Motor Subassembly:** This assembly integrates the EaglePower brushless motor with the **sun gear**. The motor is securely attached to a back plate, which also provides mounting provisions for the ODrive S1 controller. Precise positioning of the ODrive is essential to ensure optimal alignment with the onboard encoder and magnet for accurate position feedback.
    <p align="center">
      <img src="images/MOTOR_ASSY.jpg" alt="Motor Subassembly" width="600">
      <br>
      <em>Figure 8: The Motor Subassembly, illustrating the brushless motor, sun gear attachment, ODrive S1 controller, and the 6mm Neodymium magnet used for encoder feedback.</em>
    </p>

### Design Notes

* The actuator's modular design, composed of 4 main slip-on assemblies, enhances ease of construction and maintenance.
* Variations for different end effectors were included in the design, streamlining testing procedures and minimizing potential error sources.
* The actuator housing integrates passive cooling holes to help manage heat during operation.
* The ODrive S1 controller's mounting provisions are carefully designed to ensure the critical 0.5-3mm spacing from the motor's magnet for reliable onboard encoder operation.

## Manufacturing & 3D Printing Notes

Utilizing FDM 3D printing for the SHACTUATOR's components brought both advantages and specific considerations:

* **Slip-Fit Tolerances:** When designing circular slip-fit parts, such as bearing seats on 3D printed components, it was observed that oversizing the printed part by **1-2%** generally yields an optimal interference fit. This helps compensate for common 3D printing dimensional inaccuracies and ensures secure seating of components.
* **Mid-Print Bearing Insertion:** For the planetary carriers, a unique assembly step was required: the 3D print had to be paused partway through its fabrication to allow for the precise insertion of the small roller bearings. This ensures the bearings are fully encapsulated within the printed structure.

## Assembly

The assembly process for the SHACTUATOR was significantly simplified by its modular design, allowing for a logical and systematic integration of components.

<p align="center">
  <img src="images/ASSEMBLY_1.jpg" alt="Initial Assembly Phase" width="600">
  <br>
  <em>Figure 9: Initial assembly phase, showing the integration of the main bearing into the housing, highlighting the wooden rod used for stability during early tests.</em>
</p>

<p align="center">
  <img src="images/ASSEMBLY_2.jpg" alt="Planetary Carrier Insertion" width="600">
  <br>
  <em>Figure 10: Assembling the planetary carrier subassembly into the main housing, showcasing the helical planet gears.</em>
</p>

<p align="center">
  <img src="images/ASSEMBLY_3.jpg" alt="Actuator Assembly with Wooden Rod" width="600">
  <br>
  <em>Figure 11: The actuator assembly with the wooden rod fully integrated, demonstrating the early testing setup.</em>
</p>

<p align="center">
  <img src="images/ASSEMBLY_4.jpg" alt="Motor and ODrive Integration" width="600">
  <br>
  <em>Figure 12: Integrating the motor and ODrive controller into the actuator housing, completing the core electromechanical assembly.</em>
</p>

## Electronics & Control Setup

The SHACTUATOR's intelligent control is handled by the **ODrive S1 Controller**, which precisely manages the EaglePower brushless motor. For position feedback, the motor leverages its onboard encoder in conjunction with a 6mm Neodymium magnet. Crucially, the ODrive Technical Specification recommends maintaining a spacing of **0.5 to 3mm** between the top surface of the encoder IC and the magnet for optimal performance and signal integrity.

<p align="center">
  <img src="images/image_5c3c82.png" alt="Encoder Magnet Spacing" width="500">
  <br>
  <em>Figure 13: Diagram illustrating the recommended spacing (0.5 - 3mm) between the ODrive encoder and the magnet for optimal position sensing.</em>
</p>

During the testing and tuning phases, control was exclusively managed via the **ODrive Dashboard**. This intuitive graphical user interface allowed for direct setting of motor positions, velocities, or torques, eliminating the need for custom coding to conduct performance assessments.

### ODrive Tuning

Optimal performance of the SHACTUATOR was achieved through careful tuning of the ODrive S1 controller's proportional-integral-derivative (PID) gains, referencing the comprehensive ODrive Documentation. The following gain values provided the best results for actuator response and damping characteristics:

* **Position Gain:** 156 (rev/s)/rev)
* **Velocity Gain:** 0.552 Nm/(rev/s)
* **Velocity Integrator Gain:** 0.05 (Nm/s)/(rev/s)

<p align="center">
  <img src="images/image_5c3ca7.png" alt="ODrive Dashboard Tuning" width="700">
  <br>
  <em>Figure 14: Screenshot of the ODrive Dashboard showing the configured PID gain values (Position, Velocity, and Velocity Integrator Gain) and the resultant position, velocity, and current damping curves during testing.</em>
</p>

## Testing & Performance

Rigorous testing was conducted to characterize the SHACTUATOR's performance across various parameters, providing valuable insights into its capabilities and limitations.

### Max Torque Test

* **Methodology:** The actuator's maximum torque output was assessed using a handheld force gauge at a marked distance from the actuator's rotation axis.
* **Results:** In the low current limit stages, the actuator exhibited linear behavior, with actual torque closely aligning with the theoretical $T = (k_t)(I)$ relationship. However, from 15A and beyond, a noticeable deviation from the expected linear trend was observed, indicating some loss. This phenomenon is commonly attributed to material friction losses (e.g., from bearings or gear meshing) and heat generation, particularly at higher torques and currents, a finding consistent with existing motor torque literature. Our final actuator torque was calculated to be **11.68 ft-lbs**.

<p align="center">
  <img src="images/TORQUE_RESULTS.png" alt="Torque vs Current Limit" width="700">
  <br>
  <em>Figure 15: Torque vs Current Limit graph, comparing measured performance against projected linear behavior, highlighting the onset of losses at higher current thresholds.</em>
</p>

<p align="center">
  <img src="images/MOTOR_TORQUE_CALC.JPEG" alt="Motor Torque Calculation" width="600">
  <br>
  <em>Figure 16: Detailed motor torque calculations, including the derivation of the torque constant (kt) and the final actuator torque, incorporating an assumed 80% efficiency for the system.</em>
</p>

### Compliance & Backdrivability

* **Methodology:** The actuator's inherent compliance and backdrivability were qualitatively tested at various torque ratings: 4, 7.5, and 14 ft-lb.
* **Results:** Across all tested torque setups, the SHACTUATOR proved to be backdrivable, meaning it could be moved by external forces. Furthermore, it demonstrated excellent damping characteristics after careful tuning of the ODrive controller's gains. As anticipated, backdriving was significantly easier at lower torque settings. This outcome was highly satisfactory, as it successfully proved the actuator's compliance, making it a strong candidate for applications requiring compliant joints, such as a robotic dog.

### Speed Tests

* **Results:** Performance tests showed that the motor can reach a peak speed of **1920 rpm** before encountering the upper current limit of the desktop power supply. The actuator is capable of maintaining a continuous speed of **1200 rpm** under no-load conditions.
* **Power Supply Configuration:** During these tests, the power supply was set to 24V (with a maximum capacity of 30V) and its output current limit was set to its maximum of 10A. The motor itself has a peak continuous current rating of 22A.

### Continuous Torque Test

* **Methodology:** To assess the actuator's ability to sustain torque over time, a continuous torque test was devised. Given the motor's specified continuous current limit of 22A, which translates to approximately 10 ft-lbs from our torque graph, a 5lb dumbbell was attached to a weighted band. The SHACTUATOR then performed a series of "robot curls" to evaluate its endurance under continuous load.

### Backlash Evaluation

* **Results:** Moderate backlash was qualitatively detected in the system. While precise quantification was not possible without a strain gauge, the observed backlash was deemed to be very little, which is a positive indicator for a 3D-printed gearbox.

## Challenges & Lessons Learned

Developing the SHACTUATOR provided valuable insights and highlighted several critical challenges inherent in high-performance custom mechatronic systems.

### Power Supply Limitations

During higher current testing, particularly above 35A, the desktop power supply used reached its upper capability limit. This constraint prevented us from fully characterizing the motor's performance at its highest operational currents and understanding its behavior under more extreme loads. Moving forward, a more robust power supply will be essential.

### Material Strain

An early design hurdle emerged at around 15A during torque tests: the PLA printed rod and the round actuator housing, secured by wood clamps, proved unable to maintain stability. This necessitated a quick pivot to reinforce the system. The original PLA rod was reprinted using wood, significantly improving stability for subsequent tests. This experience underscored the importance of material selection and robust mechanical fixturing, especially when pushing 3D printed components to their limits, and suggested potential friction and heat losses in the printed material itself at higher torques.

## Future Improvements

Based on the insights gained from this project, several avenues for future improvement have been identified to enhance the SHACTUATOR's performance and capabilities:

* **Reduce Backlash:** A key improvement for future revisions will involve increasing the preload in the gear teeth. This mechanical adjustment is expected to significantly reduce the observed backlash, leading to more precise motion control.
* **Enhanced Power Supply:** To fully unlock the EaglePower motor's potential and conduct comprehensive testing beyond 35A, investing in a higher-capacity power supply is a priority.
* **Advanced Control & Thermal Management:** While good damping was achieved, exploring more sophisticated control strategies could further optimize performance. Additionally, integrating a thermistor for continuous temperature monitoring would provide crucial data for thermal management, especially under sustained high-torque operation.
* **Quantitative Data Collection:** Implementing dedicated instrumentation, such as strain gauges, would enable the quantitative measurement of compliance and backlash, providing precise performance metrics that were not achievable in this phase.
* **Full Robotic Integration:** The promising compliance results, particularly for a robotic dog application, suggest that the next logical step is to integrate the SHACTUATOR into a complete robotic platform, testing its performance in a real-world multi-joint system.

## CAD Models

The CAD models (STP files) for the SHACTUATOR, including all assemblies and individual components, are attached to this repository. These models provide comprehensive details for replication, modification, or further development.
