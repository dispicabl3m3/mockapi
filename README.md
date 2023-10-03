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

import { ModelAndView } from '../models/modelAndView';

import { BASE_PATH } from './variables';
import { Configuration } from './configuration';


@Injectable()
export class BasicErrorControllerService {

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
     * errorHtml
     *
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public errorHtmlUsingDELETE(observe?: 'body', reportProgress?: boolean): Observable<ModelAndView>;
    public errorHtmlUsingDELETE(observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<ModelAndView>>;
    public errorHtmlUsingDELETE(observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<ModelAndView>>;
    public errorHtmlUsingDELETE(observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            'text/html'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
        ];

        return this.httpClient.delete<ModelAndView>(`${this.basePath}/error`,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * errorHtml
     *
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public errorHtmlUsingGET(observe?: 'body', reportProgress?: boolean): Observable<ModelAndView>;
    public errorHtmlUsingGET(observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<ModelAndView>>;
    public errorHtmlUsingGET(observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<ModelAndView>>;
    public errorHtmlUsingGET(observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            'text/html'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
        ];

        return this.httpClient.get<ModelAndView>(`${this.basePath}/error`,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * errorHtml
     *
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public errorHtmlUsingHEAD(observe?: 'body', reportProgress?: boolean): Observable<ModelAndView>;
    public errorHtmlUsingHEAD(observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<ModelAndView>>;
    public errorHtmlUsingHEAD(observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<ModelAndView>>;
    public errorHtmlUsingHEAD(observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            'text/html'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];

        return this.httpClient.head<ModelAndView>(`${this.basePath}/error`,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * errorHtml
     *
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public errorHtmlUsingOPTIONS(observe?: 'body', reportProgress?: boolean): Observable<ModelAndView>;
    public errorHtmlUsingOPTIONS(observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<ModelAndView>>;
    public errorHtmlUsingOPTIONS(observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<ModelAndView>>;
    public errorHtmlUsingOPTIONS(observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            'text/html'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];

        return this.httpClient.options<ModelAndView>(`${this.basePath}/error`,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * errorHtml
     *
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public errorHtmlUsingPATCH(observe?: 'body', reportProgress?: boolean): Observable<ModelAndView>;
    public errorHtmlUsingPATCH(observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<ModelAndView>>;
    public errorHtmlUsingPATCH(observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<ModelAndView>>;
    public errorHtmlUsingPATCH(observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            'text/html'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];

        return this.httpClient.patch<ModelAndView>(`${this.basePath}/error`,
            null,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * errorHtml
     *
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public errorHtmlUsingPOST(observe?: 'body', reportProgress?: boolean): Observable<ModelAndView>;
    public errorHtmlUsingPOST(observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<ModelAndView>>;
    public errorHtmlUsingPOST(observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<ModelAndView>>;
    public errorHtmlUsingPOST(observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            'text/html'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];

        return this.httpClient.post<ModelAndView>(`${this.basePath}/error`,
            null,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

    /**
     * errorHtml
     *
     * @param observe set whether or not to return the data Observable as the body, response or events. defaults to returning the body.
     * @param reportProgress flag to report request and response progress.
     */
    public errorHtmlUsingPUT(observe?: 'body', reportProgress?: boolean): Observable<ModelAndView>;
    public errorHtmlUsingPUT(observe?: 'response', reportProgress?: boolean): Observable<HttpResponse<ModelAndView>>;
    public errorHtmlUsingPUT(observe?: 'events', reportProgress?: boolean): Observable<HttpEvent<ModelAndView>>;
    public errorHtmlUsingPUT(observe: any = 'body', reportProgress: boolean = false ): Observable<any> {

        let headers = this.defaultHeaders;

        // to determine the Accept header
        const httpHeaderAccepts: string[] = [
            'text/html'
        ];
        const httpHeaderAcceptSelected: string | undefined = this.configuration.selectHeaderAccept(httpHeaderAccepts);
        if (httpHeaderAcceptSelected !== undefined) {
            headers = headers.set('Accept', httpHeaderAcceptSelected);
        }

        // to determine the Content-Type header
        const consumes: string[] = [
            'application/json'
        ];

        return this.httpClient.put<ModelAndView>(`${this.basePath}/error`,
            null,
            {
                withCredentials: this.configuration.withCredentials,
                headers,
                observe,
                reportProgress
            }
        );
    }

}
