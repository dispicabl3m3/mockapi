package com.hcsc.claims.uis.util;

import java.util.ArrayList;
import java.util.Collections;
import java.util.HashSet;
import java.util.List;
import java.util.Set;

import javax.annotation.PostConstruct;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.stereotype.Service;

import com.hcsc.claims.uis.enums.aom.ClaimIncrementReasonCode;
import com.hcsc.claims.uis.enums.aom.ClaimStatusCode;
import com.hcsc.claims.uis.model.aom.ReferenceDomainDescription;
import com.hcsc.claims.uis.model.aom.ReferenceDomainDescriptionFields;
import com.hcsc.claims.uis.model.aom.ReferenceDomainName;

@Service
public class ClaimStatusCodeSubSet {

  private static final Logger LOGGER = LoggerFactory.getLogger(ClaimStatusCodeSubSet.class);

  private Set<String> incrementReasonCodes;

  private Set<String> pendStatusCodes;

  private Set<String> withdrawStatusCodes;

  private Set<String> releaseStatusCodes;

  private Set<String> denyStatusCodes;

  private Set<String> finalizedStatusCodes;

  private Set<String> closeStatusCodes;

  @PostConstruct
  public void init() {
    incrementReasonCodes = new HashSet<>();
    for (ClaimIncrementReasonCode reasonCode : ClaimIncrementReasonCode.values()) {
      incrementReasonCodes.add(reasonCode.code());
    }
    incrementReasonCodes = Collections.unmodifiableSet(incrementReasonCodes);

    pendStatusCodes = new HashSet<>();
    pendStatusCodes.add(ClaimStatusCode.Pend_pre_payment_COB_investigation.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_COB_awaiting_COB_system_update.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_group_with_converted_history_claims_membership_denied_with_FSS_information.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_pre_payment_D_and_R_investigation.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_pre_payment_subrogation_investigation.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_awaiting_response_from_Control_Plan_used_when_claim_is_processed_by_an_operator.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_stat_debit_awaiting_FSS_item.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_claim_release.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_membership_processing.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_patient_processing.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_provider_processing.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_service_processing.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_COB_screen.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_awaiting_FSS_item_correction.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_workers_compensation_processing.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_Medicare_processing.code());
    pendStatusCodes.add(ClaimStatusCode.Pend_advance_check_awaiting_FSS_item.code());
    pendStatusCodes = Collections.unmodifiableSet(pendStatusCodes);

    withdrawStatusCodes = new HashSet<>();
    withdrawStatusCodes.add(ClaimStatusCode.Withdrawn_registered_in_error.code());
    withdrawStatusCodes.add(ClaimStatusCode.Withdrawn_need_provider_information.code());
    withdrawStatusCodes.add(ClaimStatusCode.Withdrawn_need_membership_information.code());
    withdrawStatusCodes.add(ClaimStatusCode.Withdrawn_need_patient_information.code());
    withdrawStatusCodes.add(ClaimStatusCode.Withdrawn_need_claim_level_information.code());
    withdrawStatusCodes.add(ClaimStatusCode.Withdrawn_need_service_information.code());
    withdrawStatusCodes.add(ClaimStatusCode.Withdrawn_from_pend.code());
    withdrawStatusCodes = Collections.unmodifiableSet(withdrawStatusCodes);

    releaseStatusCodes = new HashSet<>();
    releaseStatusCodes.add(ClaimStatusCode.Paid.code());
    releaseStatusCodes.add(ClaimStatusCode.Advance_check_or_manual_check.code());
    releaseStatusCodes.add(ClaimStatusCode.Paid_post_payment_COB_investigation.code());
    releaseStatusCodes.add(ClaimStatusCode.BIS_claim_paid.code());
    releaseStatusCodes = Collections.unmodifiableSet(releaseStatusCodes);

    denyStatusCodes = new HashSet<>();
    denyStatusCodes.add(ClaimStatusCode.Disapproved_after_service.code());
    denyStatusCodes.add(ClaimStatusCode.Disapproved_before_service_membership.code());
    denyStatusCodes.add(ClaimStatusCode.Disapproved_for_membership.code());
    denyStatusCodes.add(ClaimStatusCode.Disapproved_for_patient.code());
    denyStatusCodes.add(ClaimStatusCode.Disapproved_for_provider.code());
    denyStatusCodes.add(ClaimStatusCode.Disapproved_claim_level_data_for_incorrect_discount_information.code());
    denyStatusCodes.add(ClaimStatusCode.BIS_claim_disapproved.code());
    denyStatusCodes = Collections.unmodifiableSet(denyStatusCodes);

    finalizedStatusCodes = new HashSet<>();
    finalizedStatusCodes.add(ClaimStatusCode.Paid.code());
    finalizedStatusCodes.add(ClaimStatusCode.Advance_check_or_manual_check.code());
    finalizedStatusCodes.add(ClaimStatusCode.Statistical_Debit_no_additional_payment.code());
    finalizedStatusCodes.add(ClaimStatusCode.Statistical_Debit_with_additional_payment.code());
    finalizedStatusCodes.add(ClaimStatusCode.Group_with_converted_history_claims_with_no_additional_payment.code());
    finalizedStatusCodes.add(ClaimStatusCode.Group_with_converted_history_claim_with_additional_payment.code());
    finalizedStatusCodes.add(ClaimStatusCode.Issued_no_payment.code());
    finalizedStatusCodes.add(ClaimStatusCode.BIS_claim_paid.code());
    finalizedStatusCodes.add(ClaimStatusCode.BIS_claim_disapproved.code());
    finalizedStatusCodes = Collections.unmodifiableSet(finalizedStatusCodes);

    closeStatusCodes = new HashSet<>();
    closeStatusCodes.add(ClaimStatusCode.Claim_closed_for_COB_investigation_issued_no_payment.code());
    closeStatusCodes.add(ClaimStatusCode.Claim_in_a_transmission_only_status_considered_closed.code());
    closeStatusCodes.add(ClaimStatusCode.Closed_claim_statistical_change.code());
    closeStatusCodes = Collections.unmodifiableSet(closeStatusCodes);

  }

  public void populateClaimStatusByDisposition(ReferenceDomainName container) {
    List<ReferenceDomainDescriptionFields> claimStatus = container.getClaimStatus().getDataList();

    List<ReferenceDomainDescriptionFields> incrementStatus = new ArrayList<ReferenceDomainDescriptionFields>();
    List<ReferenceDomainDescriptionFields> pendStatus = new ArrayList<ReferenceDomainDescriptionFields>();
    List<ReferenceDomainDescriptionFields> withdrawStatus = new ArrayList<ReferenceDomainDescriptionFields>();
    List<ReferenceDomainDescriptionFields> releaseStatus = new ArrayList<ReferenceDomainDescriptionFields>();
    List<ReferenceDomainDescriptionFields> denyStatus = new ArrayList<ReferenceDomainDescriptionFields>();
    List<ReferenceDomainDescriptionFields> finalizedStatus = new ArrayList<ReferenceDomainDescriptionFields>();
    List<ReferenceDomainDescriptionFields> closeStatus = new ArrayList<ReferenceDomainDescriptionFields>();

    for (ReferenceDomainDescriptionFields reference : claimStatus) {
      if (this.pendStatusCodes.contains(reference.getValue())) {
        pendStatus.add(reference);
      }
      if (this.incrementReasonCodes.contains(reference.getValue())) {
        incrementStatus.add(reference);
      }
      if (this.withdrawStatusCodes.contains(reference.getValue())) {
        withdrawStatus.add(reference);
      }
      if (this.releaseStatusCodes.contains(reference.getValue())) {
        releaseStatus.add(reference);
      }
      if (this.denyStatusCodes.contains(reference.getValue())) {
        denyStatus.add(reference);
      }
      if (this.finalizedStatusCodes.contains(reference.getValue())) {
        finalizedStatus.add(reference);
      }
      if (this.closeStatusCodes.contains(reference.getValue())) {
        closeStatus.add(reference);
      }
    }

    ReferenceDomainDescription pendStatusStore = new ReferenceDomainDescription();
    pendStatusStore.addData(pendStatus);
    container.setClaimPendStatus(pendStatusStore);
    LOGGER.debug("Pend status store: {}", pendStatusStore);

    ReferenceDomainDescription incrementStatusStore = new ReferenceDomainDescription();
    incrementStatusStore.addData(incrementStatus);
    container.setClaimIncrementStatus(incrementStatusStore);
    LOGGER.debug("Increment status store: {}", incrementStatusStore);

    ReferenceDomainDescription withdrawStatusStore = new ReferenceDomainDescription();
    withdrawStatusStore.addData(withdrawStatus);
    container.setClaimWithdrawStatus(withdrawStatusStore);
    LOGGER.debug("Withdraw status store: {}", withdrawStatusStore);

    ReferenceDomainDescription releaseStatusStore = new ReferenceDomainDescription();
    releaseStatusStore.addData(releaseStatus);
    container.setClaimReleaseStatus(releaseStatusStore);
    LOGGER.debug("Release status store: {}", releaseStatusStore);

    ReferenceDomainDescription denyStatusStore = new ReferenceDomainDescription();
    denyStatusStore.addData(denyStatus);
    container.setClaimDenyStatus(denyStatusStore);
    LOGGER.debug("Deny status store: {}", denyStatusStore);

    ReferenceDomainDescription finalizedStatusStore = new ReferenceDomainDescription();
    finalizedStatusStore.addData(finalizedStatus);
    container.setClaimFinalizedStatus(finalizedStatusStore);
    LOGGER.debug("Finalized status store: {}", finalizedStatusStore);

    ReferenceDomainDescription closeStatusStore = new ReferenceDomainDescription();
    closeStatusStore.addData(closeStatus);
    container.setClaimCloseStatus(closeStatusStore);
    LOGGER.debug("Close status store: {}", closeStatusStore);
  }

  public Set<String> getIncrementReasonCodes() {
    return incrementReasonCodes;
  }

  public Set<String> getPendStatusCodes() {
    return pendStatusCodes;
  }

  public Set<String> getWithdrawStatusCodes() {
    return withdrawStatusCodes;
  }

  public Set<String> getReleaseStatusCodes() {
    return releaseStatusCodes;
  }

  public Set<String> getDenyStatusCodes() {
    return denyStatusCodes;
  }

  public Set<String> getFinalizedStatusCodes() {
    return finalizedStatusCodes;
  }

  public Set<String> getCloseStatusCodes() {
    return closeStatusCodes;
  }
}
