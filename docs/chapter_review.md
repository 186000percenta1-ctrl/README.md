import 'package:flutter/material.dart';

void main() {
  runApp(const AutomotiveServiceApp());
}

class AutomotiveServiceApp extends StatelessWidget {
  const AutomotiveServiceApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Automotive Service Timeline',
      theme: ThemeData(
        useMaterial3: true,
        colorScheme: ColorScheme.fromSeed(
          seedColor: Colors.blue,
        ),
        scaffoldBackgroundColor: const Color(0xFFF5F7FA),
      ),
      home: const ServiceTimelineScreen(),
    );
  }
}

class ServiceStep {
  final int number;
  final String title;
  final String description;
  final IconData icon;
  final List<String> details;

  const ServiceStep({
    required this.number,
    required this.title,
    required this.description,
    required this.icon,
    this.details = const [],
  });
}

class ServiceTimelineScreen extends StatefulWidget {
  const ServiceTimelineScreen({super.key});

  @override
  State<ServiceTimelineScreen> createState() =>
      _ServiceTimelineScreenState();
}

class _ServiceTimelineScreenState
    extends State<ServiceTimelineScreen> {
  int completedSteps = 0;

  final List<ServiceStep> steps = const [
    ServiceStep(
      number: 1,
      title: 'Customer Arrival',
      description:
          'Customer arrives at the dealership or repair facility.',
      icon: Icons.directions_car,
    ),
    ServiceStep(
      number: 2,
      title: 'Initial Greeting',
      description:
          'The Service Advisor greets the customer, gathers information, and begins building trust.',
      icon: Icons.handshake,
      details: [
        'Customer name',
        'Address',
        'Vehicle history',
        'Reason for visit',
        'Establish customer relationship',
      ],
    ),
    ServiceStep(
      number: 3,
      title: 'Walk-Around Inspection',
      description:
          'The Service Advisor inspects the vehicle with the customer when possible.',
      icon: Icons.search,
      details: [
        'Document existing damage',
        'Check tires',
        'Check wipers',
        'Check fluid levels',
        'Identify potential service needs',
      ],
    ),
    ServiceStep(
      number: 4,
      title: 'Repair Order Creation',
      description:
          'The Service Advisor collects the information required to create the repair order.',
      icon: Icons.description,
      details: [
        'Customer-requested work',
        'Vehicle information',
        'Additional recommendations',
      ],
    ),
    ServiceStep(
      number: 5,
      title: 'Cost Estimate & Approval',
      description:
          'The customer receives an estimate, reviews the repair order, and provides authorization.',
      icon: Icons.request_quote,
      details: [
        'Explain repair order',
        'Provide estimated cost',
        'Obtain customer approval',
        'Establish authorized dollar amount',
      ],
    ),
    ServiceStep(
      number: 6,
      title: 'Technician Inspection & Diagnosis',
      description:
          'The technician inspects the vehicle, performs diagnostics, and records findings.',
      icon: Icons.build,
      details: [
        'Deliver customer concerns to technician',
        'Perform multipoint inspection',
        'Diagnose reported problems',
        'Record findings',
        'Use Green / Yellow / Red recommendations',
      ],
    ),
    ServiceStep(
      number: 7,
      title: 'Reporting the Diagnosis',
      description:
          'The Service Advisor communicates the technician findings to the customer.',
      icon: Icons.phone_in_talk,
      details: [
        'Address the original concern first',
        'Explain essential safety recommendations',
        'Discuss other recommended services',
      ],
    ),
    ServiceStep(
      number: 8,
      title: 'Quote Presentation',
      description:
          'The Service Advisor presents a detailed repair quote.',
      icon: Icons.receipt_long,
      details: [
        'Labor costs',
        'Parts costs',
        'Expected repair time',
      ],
    ),
    ServiceStep(
      number: 9,
      title: 'Closing the Sale',
      description:
          'The Service Advisor answers questions, addresses concerns, and seeks authorization.',
      icon: Icons.check_circle_outline,
      details: [
        'Answer customer questions',
        'Address concerns',
        'Explain recommended repairs',
        'Obtain approval',
      ],
    ),
    ServiceStep(
      number: 10,
      title: 'Vehicle Handoff',
      description:
          'Once repairs are authorized, the Service Advisor communicates the expected repair or diagnostic timeline.',
      icon: Icons.key,
    ),
    ServiceStep(
      number: 11,
      title: 'Service & Repair',
      description:
          'Technicians perform the authorized services and repairs.',
      icon: Icons.car_repair,
    ),
    ServiceStep(
      number: 12,
      title: 'Vehicle Delivery',
      description:
          'The repaired vehicle is delivered back to the customer.',
      icon: Icons.local_shipping,
      details: [
        'Review completed work',
        'Review inspection report',
        'Prioritize future recommendations',
        'Explain Green / Yellow / Red items',
        'Provide survey or promotional information when applicable',
        'Schedule a return appointment if needed',
      ],
    ),
    ServiceStep(
      number: 13,
      title: 'Payment & Invoice',
      description:
          'The customer pays for the services and the advisor reviews the invoice.',
      icon: Icons.payments,
      details: [
        'Review final invoice',
        'Explain charges',
        'Collect payment',
      ],
    ),
    ServiceStep(
      number: 14,
      title: 'Follow-Up',
      description:
          'The Service Advisor follows up to collect feedback and confirm customer satisfaction.',
      icon: Icons.follow_the_signs,
      details: [
        'Customer survey',
        'Phone follow-up',
        'Gather feedback',
        'Confirm satisfaction',
      ],
    ),
  ];

  void toggleCompleted(int index) {
    setState(() {
      if (index < completedSteps) {
        completedSteps = index;
      } else {
        completedSteps = index + 1;
      }
    });
  }

  @override
  Widget build(BuildContext context) {
    final progress = completedSteps / steps.length;

    return Scaffold(
      appBar: AppBar(
        title: const Text(
          'Automotive Service Timeline',
          style: TextStyle(fontWeight: FontWeight.bold),
        ),
        centerTitle: true,
      ),
      body: Column(
        children: [
          _buildHeader(progress),
          Expanded(
            child: ListView.builder(
              padding: const EdgeInsets.all(16),
              itemCount: steps.length,
              itemBuilder: (context, index) {
                return _buildTimelineItem(
                  context,
                  index,
                  steps[index],
                );
              },
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildHeader(double progress) {
    return Container(
      width: double.infinity,
      padding: const EdgeInsets.fromLTRB(20, 16, 20, 20),
      color: Colors.white,
      child: Column(
        crossAxisAlignment: CrossAxisAlignment.start,
        children: [
          const Text(
            'Service Advising & Management',
            style: TextStyle(
              fontSize: 20,
              fontWeight: FontWeight.bold,
            ),
          ),
          const SizedBox(height: 6),
          Text(
            '$completedSteps of ${steps.length} steps completed',
            style: TextStyle(
              color: Colors.grey.shade700,
            ),
          ),
          const SizedBox(height: 12),
          ClipRRect(
            borderRadius: BorderRadius.circular(10),
            child: LinearProgressIndicator(
              value: progress,
              minHeight: 9,
            ),
          ),
        ],
      ),
    );
  }

  Widget _buildTimelineItem(
    BuildContext context,
    int index,
    ServiceStep step,
  ) {
    final isCompleted = index < completedSteps;
    final isCurrent = index == completedSteps;

    return Row(
      crossAxisAlignment: CrossAxisAlignment.start,
      children: [
        SizedBox(
          width: 55,
          child: Column(
            children: [
              GestureDetector(
                onTap: () => toggleCompleted(index),
                child: CircleAvatar(
                  radius: 23,
                  backgroundColor: isCompleted
                      ? Colors.green
                      : isCurrent
                          ? Colors.blue
                          : Colors.grey.shade300,
                  child: isCompleted
                      ? const Icon(
                          Icons.check,
                          color: Colors.white,
                        )
                      : Text(
                          '${step.number}',
                          style: TextStyle(
                            fontWeight: FontWeight.bold,
                            color: isCurrent
                                ? Colors.white
                                : Colors.black87,
                          ),
                        ),
                ),
              ),
              if (index < steps.length - 1)
                Container(
                  width: 3,
                  height: 100,
                  color: isCompleted
                      ? Colors.green
                      : Colors.grey.shade300,
                ),
            ],
          ),
        ),
        Expanded(
          child: Padding(
            padding: const EdgeInsets.only(bottom: 18),
            child: Card(
              elevation: isCurrent ? 3 : 1,
              child: ExpansionTile(
                leading: Icon(
                  step.icon,
                  color: isCompleted
                      ? Colors.green
                      : Colors.blue,
                ),
                title: Text(
                  step.title,
                  style: const TextStyle(
                    fontWeight: FontWeight.bold,
                  ),
                ),
                subtitle: Padding(
                  padding: const EdgeInsets.only(top: 5),
                  child: Text(step.description),
                ),
                children: [
                  if (step.details.isNotEmpty)
                    Padding(
                      padding: const EdgeInsets.fromLTRB(
                        20,
                        0,
                        20,
                        16,
                      ),
                      child: Column(
                        children: step.details
                            .map(
                              (detail) => ListTile(
                                dense: true,
                                contentPadding: EdgeInsets.zero,
                                leading: const Icon(
                                  Icons.arrow_right,
                                  size: 20,
                                ),
                                title: Text(detail),
                              ),
                            )
                            .toList(),
                      ),
                    ),
                  Padding(
                    padding: const EdgeInsets.only(
                      left: 20,
                      right: 20,
                      bottom: 16,
                    ),
                    child: SizedBox(
                      width: double.infinity,
                      child: FilledButton.icon(
                        onPressed: () => toggleCompleted(index),
                        icon: Icon(
                          isCompleted
                              ? Icons.undo
                              : Icons.check,
                        ),
                        label: Text(
                          isCompleted
                              ? 'Mark Incomplete'
                              : 'Mark Complete',
                        ),
                      ),
                    ),
                  ),
                ],
              ),
            ),
          ),
        ),
      ],
    );
  }
}