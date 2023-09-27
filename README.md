/**
 * Claims UI Inquiry Service API
 *
 */
/* tslint:disable:no-unused-variable member-ordering */

import { Inject, Injectable, Optional } from '@angular/core';
import {
    HttpClient, HttpHeaders, HttpParams,
    HttpResponse, HttpEvent
} from '@angular/common/http';

import { Observable } from 'rxjs/Observable';

import { ClaimsRequest } from '../models/claimsRequest';
import { CodeReferenceRequest } from '../models/codeReferenceRequest';
import { PayloadClaimsInquirySummaryResponse } from '../models/payloadClaimsInquirySummaryResponse';
import { PayloadCodeReferenceResponse } from '../models/payloadCodeReferenceResponse';
import { PayloadPatientDetailsResponse } from '../models/payloadPatientDetailsResponse';
import { PayloadProviderDetails } from '../models/payloadProviderDetails';
import { PayloadClaimDetails } from '../models/payloadClaimDetails';
import { PayloadReferenceDataResponse } from '../models/payloadReferenceDataResponse';
import { ReferenceDataRequest } from '../models/referenceDataRequest';

import { BASE_PATH } from './variables';
import { Configuration } from './configuration';


@Injectable()
export class ClaimsInquiryControllerService {

    protected basePath = 'https://claims-ui-inquiry-service-v1-uit9.cfaa.azr.hcsctest.net';
    public defaultHeaders = new HttpHeaders();
    public configuration = new Configuration();

    constructor(protected httpClient: HttpClient, @Optional()@Inject(BASE_PATH) basePath: string, @Optional() configuration: Configuration) {
        if (basePath) {
            this.basePath = basePath;
        }
        if (configuration) {
            this.configuration = configuration;
            this.basePath = basePath || configuration.basePath || this.basePath;
        }
    }

    /**
     * @param consumes string[] mime-types
     * @return true: consumes contains 'multipart/form-data', false: otherwise
     */
    private canConsumeForm(consumes: string[]): boolean {
        const form = 'multipart/form-data';
        for (const consume of consumes) {
            if (form === consume) {
                return true;
            }
        }
        return false;
    }


    /**
     * getClaimSummary
     *
     * @param claimsRequest Generic Post request body that can be used while searching claim related data using claimId or DCN + received Date
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public getClaimSummaryUsingPOST(claimsRequest: ClaimsRequest, observe?: 'body', reportProgress?: boolean): Observable<PayloadClaimsInquirySummaryResponse>;
    public getClaimSummaryUsingPOST(claimsRequest: ClaimsRequest, observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<PayloadClaimsInquirySummaryResponse>>;
    public getClaimSummaryUsingPOST(claimsRequest: ClaimsRequest, observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<PayloadClaimsInquirySummaryResponse>>;
    public getClaimSummaryUsingPOST(claimsRequest: ClaimsRequest, observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        if (claimsRequest === null || claimsRequest === undefined) {
            throw new Error('Required parameter claimsRequest was null or undefined when calling getClaimSummaryUsingPOST.');
        }

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            '*/*'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];
        const httpContentTypeSelected: string | undefined = this.configuration.selectHeaderContentType(consumes);
        if (httpContentTypeSelected !== undefined) {
            headers = headers.set('Content-Type', httpContentTypeSelected);
        }

        return this.httpClient.post<PayloadClaimsInquirySummaryResponse>(`${this.basePath}/claims/v1/claim-summary`,
            claimsRequest,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * getCodeReference
     *
     * @param codeReferenceRequest Code Reference Request
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public getCodeReferenceUsingPOST(codeReferenceRequest: CodeReferenceRequest, observe?: 'body', reportProgress?: boolean): Observable<PayloadCodeReferenceResponse>;
    public getCodeReferenceUsingPOST(codeReferenceRequest: CodeReferenceRequest, observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<PayloadCodeReferenceResponse>>;
    public getCodeReferenceUsingPOST(codeReferenceRequest: CodeReferenceRequest, observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<PayloadCodeReferenceResponse>>;
    public getCodeReferenceUsingPOST(codeReferenceRequest: CodeReferenceRequest, observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        if (codeReferenceRequest === null || codeReferenceRequest === undefined) {
            throw new Error('Required parameter codeReferenceRequest was null or undefined when calling getCodeReferenceUsingPOST.');
        }

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            '*/*'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];
        const httpContentTypeSelected: string | undefined = this.configuration.selectHeaderContentType(consumes);
        if (httpContentTypeSelected !== undefined) {
            headers = headers.set('Content-Type', httpContentTypeSelected);
        }

        return this.httpClient.post<PayloadCodeReferenceResponse>(`${this.basePath}/claims/v1/code-reference`,
            codeReferenceRequest,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * getPatientDetails
     *
     * @param claimsRequest Generic Post request body that can be used while searching claim related data using claimId or DCN + received Date
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public getPatientDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'body', reportProgress?: boolean): Observable<PayloadPatientDetailsResponse>;
    public getPatientDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<PayloadPatientDetailsResponse>>;
    public getPatientDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<PayloadPatientDetailsResponse>>;
    public getPatientDetailsUsingPOST(claimsRequest: ClaimsRequest, observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        if (claimsRequest === null || claimsRequest === undefined) {
            throw new Error('Required parameter claimsRequest was null or undefined when calling getPatientDetailsUsingPOST.');
        }

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            '*/*'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];
        const httpContentTypeSelected: string | undefined = this.configuration.selectHeaderContentType(consumes);
        if (httpContentTypeSelected !== undefined) {
            headers = headers.set('Content-Type', httpContentTypeSelected);
        }

        return this.httpClient.post<PayloadPatientDetailsResponse>(`${this.basePath}/claims/v1/patient-details`,
            claimsRequest,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * getProviderDetails
     *
     * @param claimsRequest Generic Post request body that can be used while searching claim related data using claimId or DCN + received Date
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public getProviderDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'body', reportProgress?: boolean): Observable<PayloadProviderDetails>;
    public getProviderDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<PayloadProviderDetails>>;
    public getProviderDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<PayloadProviderDetails>>;
    public getProviderDetailsUsingPOST(claimsRequest: ClaimsRequest, observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        if (claimsRequest === null || claimsRequest === undefined) {
            throw new Error('Required parameter claimsRequest was null or undefined when calling getProviderDetailsUsingPOST.');
        }

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            '*/*'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];
        const httpContentTypeSelected: string | undefined = this.configuration.selectHeaderContentType(consumes);
        if (httpContentTypeSelected !== undefined) {
            headers = headers.set('Content-Type', httpContentTypeSelected);
        }

        return this.httpClient.post<PayloadProviderDetails>(`${this.basePath}/claims/v1/provider-details`,
            claimsRequest,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * getClaimDetails
     *
     * @param claimsRequest Generic Post request body that can be used while searching claim related data using claimId or DCN + received Date
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public getClaimDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'body', reportProgress?: boolean): Observable<PayloadClaimDetails>;
    public getClaimDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<PayloadClaimDetails>>;
    public getClaimDetailsUsingPOST(claimsRequest: ClaimsRequest, observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<PayloadClaimDetails>>;
    public getClaimDetailsUsingPOST(claimsRequest: ClaimsRequest, observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        if (claimsRequest === null || claimsRequest === undefined) {
            throw new Error('Required parameter claimsRequest was null or undefined when calling getClaimDetailsUsingPOST.');
        }

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            '*/*'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];
        const httpContentTypeSelected: string | undefined = this.configuration.selectHeaderContentType(consumes);
        if (httpContentTypeSelected !== undefined) {
            headers = headers.set('Content-Type', httpContentTypeSelected);
        }

        return this.httpClient.post<PayloadClaimDetails>(`${this.basePath}/claims/v1/claim-details`,
            claimsRequest,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }


    /**
     * getReferenceData
     *
     * @param referenceDataRequest Provides code desciption based on domain and code
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public getReferenceDataUsingPOST(referenceDataRequest: ReferenceDataRequest, observe?: 'body', reportProgress?: boolean): Observable<PayloadReferenceDataResponse>;
    public getReferenceDataUsingPOST(referenceDataRequest: ReferenceDataRequest, observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<PayloadReferenceDataResponse>>;
    public getReferenceDataUsingPOST(referenceDataRequest: ReferenceDataRequest, observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<PayloadReferenceDataResponse>>;
    public getReferenceDataUsingPOST(referenceDataRequest: ReferenceDataRequest, observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        if (referenceDataRequest === null || referenceDataRequest === undefined) {
            throw new Error('Required parameter referenceDataRequest was null or undefined when calling getReferenceDataUsingPOST.');
        }

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            '*/*'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];
        const httpContentTypeSelected: string | undefined = this.configuration.selectHeaderContentType(consumes);
        if (httpContentTypeSelected !== undefined) {
            headers = headers.set('Content-Type', httpContentTypeSelected);
        }

        return this.httpClient.post<PayloadReferenceDataResponse>(`${this.basePath}/claims/v1/reference-data`,
            referenceDataRequest,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

}
