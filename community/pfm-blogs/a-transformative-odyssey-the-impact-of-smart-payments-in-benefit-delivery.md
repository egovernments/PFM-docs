# A Transformative Odyssey: The Impact of Smart Payments in Benefit Delivery

Authors: Ritika Singh, [MSC](https://www.microsave.net/) | Prashanth Chandramouleeswaran & Ameya Ashok Naik, eGov

## Background

How far would a dollar go if it went straight to someone in need, when they need it most? With government-to-person (G2P) payments, governments increasingly disburse welfare benefits directly to individuals or households. These high-volume, low-ticket-size G2P transactions are vital for boosting financial inclusion and empowering vulnerable communities. Globally, programs like Brazil’s Bolsa Familia and Zambia’s SWL report cost savings, leak reduction, and timely payments for grant recipients through digital payments. In India, financial inclusion has been boosted through Jan Dhan bank accounts, the use of Aadhar for identity verification, and mobile payments applications enabled by UPI, creating the possibility for government schemes to incorporate Direct Benefits Transfers (DBT).

While promising, digital G2P payments remain in their early stages, and face challenges like friction in payments, information gaps, and contextual barriers. The [<mark style="color:blue;">MUKTA</mark>](#user-content-fn-1)[^1] scheme, in the state of Odisha in India, is an example of multi-stakeholder collaboration to reengineer digital systems and government policies and processes to operationalise digitally-enabled Smart Contracting and Just-in-Time Funding Systems (JiT-FS). This has led to enhanced reach, improved observability, and a clear understanding of performance bottlenecks, empowering stakeholders to continuously refine and optimise the system.&#x20;

## Admirable Goal, Administrative Friction

&#x20;[<mark style="color:blue;">MUKTA</mark>](#user-content-fn-2)[^2] is a pioneering initiative, designed to generate wage employment for vulnerable workers in urban Odisha during the COVID-19 pandemic. Rooted in community needs and responsive to local demands, MUKTA leverages existing Community Based Organizations (CBOs) to execute public works projects which are sustainable and climate resilient. These CBOs enlist wage seekers to work on these projects, generating income for the latter.&#x20;

Delayed payments to CBOs and wage seekers were a key scheme implementation challenge. Beneficiaries faced lengthy wait times, with a baseline study across two pilot Urban Local Bodies (ULBs) finding that over 50% of completed tasks were not processed for payment, and the rest encountered delays exceeding one month. Wage seekers come from low-income households, and such delays undermine the scheme’s welfare objectives.

Such delays arise largely from cumbersome, paper-based compliances, billing, and verification processes. Every step – from attendance tracking and bill submission, to verification, approvals, and payment instructions – relied on manual processes. This increased the administrative burden on local government personnel, who are often already overburdened. These long-drawn processes also resulted in underutilisation of sanctioned funding, with funds parked idle in banks and limited transparency.

## Making Processes And Payments Smarter

These challenges threatened to undermine MUKTA's goals. It was clear that a transformative intervention was required. To address these challenges, MUKTA embraced a three-phase "Smart Payment" approach:

### Discovery: Identifying Pivotal Problems in Scheme Implementation

Extensive consultations with stakeholders at each tier of government – Finance Department (FD), Housing and Urban Development (H\&UD) Department, local government officials, and CBO representatives – helped identify key requirements for completing payments under the MUKTA scheme, and administrative inefficiencies that prevented timely completion.&#x20;

Such schemes require multi-entity coordination: project definition, estimate creation, progress monitoring, and bill approval take place at the local government level; sanctioning overall fund tranches and executing electronic payments is done by the State government. A first step in the solution was identifying what information was needed for the State to disburse payments, and how it could be communicated most efficiently.  Existing Integrated Financial Management System (IFMS) and Public Finance Management System (PFMS) data standards were leveraged to develop functional requirement specifications, leading to the development of a two-part solution: [MUKTASoft](https://works.digit.org/programmes/muktasoft-v2.0), which streamlines processes and reporting by scheme implementers, and JiT-FS (Just-in-Time Funding System), which simplifies and speeds up fund disbursal.

### Design: Developing Solutions and Proposing Reforms

MUKTASoft is a workfare scheme management platform, which streamlines project management and information flow among CBOs, local government bodies, H\&UD, and FD. The expedited flow of standardised project information is key to reducing delays in payments. Key operational components of MUKTASoft include project finalisation, wage-seeker registration, digital attendance tracking, expense logging, and payment verification, all streamlined through user-friendly interfaces for different sets of users (CBO, ULB official, etc.)&#x20;

Keeping in mind the administrative burden-related challenges identified, MUKTASoft was designed to improve overall efficiency of local and state government officials by:

* Simplifying the process of project progress tracking and wage payment approval, aiming to move from over twelve steps (as identified in the baseline) to a simple three-step (maker-checker-approver) approach for each key document.
* Enhancing visibility of project progress or delays in payments, ensuring that the responsible authority/ individual takes accountability for these, and enabling them to take steps to resolve these.
* Enabling faster payments to wage seekers using smart payments through direct integration with the state IFMS

Aligning project management and scheme verifications sets the stage for integrating smart payments, utilising digital technologies such as JiT-FS for pull-based release of funds once project milestones are achieved. Core PFM principles like "single source of truth" (ensuring data accuracy), "observability" (real-time tracking of performance), and "minimising administrative burden" through smart contracts have been woven into the design of both MUKTASoft and JiT-FS, strengthening transparency, accountability, and efficiency.

### Deployment: Orchestrating a Seamless Implementation

The implementation phase required managing multiple dependencies. One of the fundamental challenges was building trust and reliability in the solution, to replace manual ways of working, by showcasing high success rates. The deployment timeline faced disruptions, and development hurdles were common initially – as is typical when new systems are integrating for the first time. Collaborative testing uncovered edge cases affecting transaction success rates, and a robust User Testing phase helped to validate various scenarios and user needs.

Checks and balances within MUKTASoft and the JiT module were introduced and implemented to address these emerging issues. For instance, at the project finalisation stage, MUKTASoft checks for availability of funds to cover the expenses of that project. This sanction validation establishes a spending ceiling before approval of projects or payments – a key control that the State Finance Department must maintain. Similarly, when payments are directly transferred to wage-seekers' bank accounts, each transaction's success or failure must be checked, and corrective measures taken where payments have failed to go through.&#x20;

Local governments, while initially hesitant, saw that using MUKTASoft for project creation, estimate approval, and work orders had tangible benefits: reduced administrative burden, fewer delays, faster payments, and enhanced accountability. With clear demonstration of the value to all stakeholders, adoption of the solution became more universal.

## Maximising Impact: Outcomes Of Successful Deployment

* **Reduced delays:** Digitising processes from attendance tracking to payment verification dramatically streamlined workflows, facilitating disbursement of payments to wage seekers and CBOs. Pilot data indicates around 60% reduction in payment disbursement time for wage seekers. Under the new system, beneficiaries are no longer waiting months to get paid, with most bills now being processed in a matter of days.
* **Enhanced efficiency:** Automation freed up local government officials from administrative burdens, allowing them to focus on project management and monitoring, leading to improved project execution and resource utilisation.
* **Transparency and data-driven decision making:** The integrated data platform enabled real-time tracking of project progress, expenditure, and beneficiary coverage, enhancing transparency and accountability for all stakeholders. For administrators, insights from real-time data facilitated informed decision-making, allowing for quicker identification and resolution of bottlenecks, and strategic allocation of constrained resources.
* **Empowering wage seekers:** Timely wage payments and improved project execution under the Smart Payment system contributed to enhanced livelihood opportunities and overall well-being for urban communities.

## Lessons Learned

With the pilot successful in 2 ULBs, the system is now being scaled to a total of 25 (out of 115) Urban Local Bodies (ULBs) in Odisha. MUKTA's journey offers valuable lessons for other G2P initiatives seeking to leverage technology for efficient PFM and inclusive development:

* **Existing infrastructure matters:** Enrolment of wage seekers is simplified by using Aadhaar for identity verification. With Aadhaar in turn linked to Jan Dhan accounts, mapping of wage seekers to bank accounts is already in place. Widespread use of UPI addresses concerns around cash in / cash out. MUKTASoft and JIT-FS are a new wave of innovations, relying on building blocks provided by IndiaStack and related reforms.
* **Process streamlining is a key lever for any tech-enabled reform:** When workflows are digitised, with automation and minimised manual intervention, the time and effort users have to spend on administrative tasks decreases, and they can focus on tasks that require human interaction or attention. At the same time, the reliability and timeliness of data improves, enabling administrators to better manage performance, and policy makers to develop data-driven plans and strategies.&#x20;
* **Active and consistent collaboration:** Strong partnerships between government, technology providers, and frontline users (including grassroots organisations) are essential for successful implementation. The solution will be used when stakeholders feel ownership over it, for which they should be involved throughout the process, with the needs they articulate being prioritised in product design.
* **Data fragmentation undermines progress at all stages:** All stakeholders must accept  a "single source of truth", which they contribute to by ensuring that all transactions take place through a single system of record. While some transition period may be needed to achieve this goal, even in this time, data should be updated in the system of record promptly, with appropriate verification / triangulation.&#x20;
* **Adoption requires users to trust the new way of working:** Adoption is not instant; extensive training and support is essential for overcoming initial resistance. As each set of stakeholders see the benefits from the new system, they will be more likely to use it, and to advocate for it with their peers. This can also be leveraged in periodic re-training, as trained resources move and new resources join the department.
* **Adaptability is essential:** Unforeseen challenges are inevitable. Embracing flexibility and a willingness to find solutions are crucial for successful implementation.

By adopting these lessons and building upon MUKTA's success, other G2P programs can unlock the transformative potential of technology to deliver effective social safety nets and empower vulnerable communities across the globe.

## Smart Payments As A Catalyst For Inclusive Development

The early success observed with smart payments for the MUKTA scheme underscores the transformative potential of technology in G2P transactions to reduce delays in service delivery and heighten public finance efficiency. It serves as a model for government agencies, prompting them to adopt Smart Payments as a catalyst for inclusive development.&#x20;

Odisha's journey sets a model for an efficient and citizen-centric benefit delivery system, emphasising the need for adaptive strategies, collaborative partnerships, and a commitment to governance principles. Tailored to the local context, the solution can progress from basic Smart Payments, encompassing digital recording of conditional payments and compliances, to a medium level incorporating workflow management systems and APIs. The ultimate moonshot solution integrates AI/ML models, smart devices, and Internet-of-Things (IoT) to revolutionise the public finance landscape.

[^1]: Mukhyamantri Karma Tatpara Abhiyan Yojana (MUKTA Yojana) is a government scheme aimed towards providing employment to the urban poor and consequently improving the employment rate of the state.

    MUKTASoft aims to improve the overall scheme efficiency of MUKTA by identifying & providing equal job opportunities to the urban poor, constructing environment-friendly projects, developing local communities and slums & planning better in the upcoming years.

[^2]: Mukhyamantri Karma Tatpara Abhiyan Yojana (MUKTA Yojana) is a government scheme aimed towards providing employment to the urban poor and consequently improving the employment rate of the state.

    MUKTASoft aims to improve the overall scheme efficiency of MUKTA by identifying & providing equal job opportunities to the urban poor, constructing environment-friendly projects, developing local communities and slums & planning better in the upcoming years.
