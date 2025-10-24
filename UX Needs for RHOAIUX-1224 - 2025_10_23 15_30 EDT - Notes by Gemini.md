Oct 23, 2025

## UX Needs for RHOAIUX-1224

Invited [Vince Conzola](mailto:vconzola@redhat.com) [Jenny Yi](mailto:yyi@redhat.com)

Attachments [UX Needs for RHOAIUX-1224](https://www.google.com/calendar/event?eid=MDc3aGoyMHZ2NjloNnBtMWVqamlvMG1yN28gdmNvbnpvbGFAcmVkaGF0LmNvbQ) 

Meeting records [Recording](https://drive.google.com/file/d/1QIqmhC5QhFbbhYoxTB1PTUG3w5FpSgTp/view?usp=drive_web) 

### Summary

Jenny Yi outlined that the model catalog, J's metrics, and model validation metrics are not fully integrated into the model serving flow due to the lack of hardware profile awareness of specific hardware types. Jenny Yi and Vince Conzola discussed automating node targeting and GPU recommendations, acknowledging that this requires OpenShift to be aware of hardware types on nodes, potentially through manual labeling by an administrator. Vince Conzola proposed a new UI approach for hardware profiles based on grouping nodes by accelerator types, which Jenny Yi confirmed would be a completely different UI. Jenny Yi and Vince Conzola concluded that further discussion with Edson or other architects is needed to determine the feasibility of incorporating hardware type awareness and node targeting.

### Details

* **Hardware Profile Awareness** Jenny Yi explained that model catalog, J's metrics, and model validation metrics cannot be fully integrated into the model serving flow because hardware profiles are not aware of the specific hardware types (e.g., H200 or A100) within them. This lack of awareness prevents insights from being passed to model serving unless an administrator manually matches hardware profiles to specific hardware types. Jenny Yi stated that Nvidia has annotations to identify hardware types, suggesting it is a feasible architectural decision to incorporate this information into hardware profiles.

* **Automating Node Targeting and GPU Recommendations** Jenny Yi discussed the need to automate the targeting of nodes based on GPU type, which would enable better insights for model serving. They also highlighted a user story where the DT team seeks GPU recommendations for training, requiring knowledge of accelerator types in hardware profiles to estimate training time. Vince Conzola suggested that an administrator would need to label nodes in Open Shift with the proper accelerator type identifier, as Open Shift might not automatically read this information.

* **OpenShift Node Visibility and UI Approaches** Jenny Yi and Vince Conzola discussed the challenge of Open Shift's awareness of hardware types on nodes and the implications for user experience if administrators are required to manually label nodes. Jenny Yi suggested adding fields to hardware profile setup if manual input is necessary, but expressed a preference for automatic detection. Vince Conzola proposed a different approach to hardware profiles, involving a node view in the UI where administrators could group specific nodes with identified accelerator types, and then automatically create hardware profiles based on these groupings. Jenny Yi confirmed that this would require a completely different UI, similar to Kubernetes Lens, which provides a one-to-one mapping of nodes in a cluster.

* **Administrative Access and Next Steps** Jenny Yi attempted to view nodes in the Open Shift console but realized that platform administrator access was insufficient; cluster administrator privileges are required to see node details. Vince Conzola confirmed that any UI allowing users to group or identify nodes with different accelerator types for hardware profile creation would necessitate cluster administrator involvement. Both agreed that further discussion with Edson or other architects is necessary to determine what is possible regarding hardware type awareness and node targeting. Jenny Yi plans to create an RFP (Request for Proposal) and pull Edson into a conversation to discuss the feasibility of these proposals.

### Suggested next steps

- [ ] Jenny Yi will use the Gemini notes to create the RFP for Edson regarding the inclusion of hardware type in hardware profiles, and then pull him into a conversation about the feasibility.  
- [ ] Jenny Yi will add Vince Conzola and anyone else interested to the conversation with Edson about the feasibility of the hardware profile changes.

*You should review Gemini's notes to make sure they're accurate. [Get tips and learn how Gemini takes notes](https://support.google.com/meet/answer/14754931)*

*Please provide feedback about using Gemini to take notes in a [short survey.](https://google.qualtrics.com/jfe/form/SV_9vK3UZEaIQKKE7A?confid=Mkvzxjwr-zijaI_A6AbdDxIYOAIIigIgABgBCA&detailid=unspecified)*