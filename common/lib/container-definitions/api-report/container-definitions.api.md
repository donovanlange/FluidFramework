## API Report File for "@fluidframework/container-definitions"

> Do not edit this file. It is a report generated by [API Extractor](https://api-extractor.com/).

```ts

import { ConnectionMode } from '@fluidframework/protocol-definitions';
import { EventEmitter } from 'events';
import { IClient } from '@fluidframework/protocol-definitions';
import { IClientConfiguration } from '@fluidframework/protocol-definitions';
import { IClientDetails } from '@fluidframework/protocol-definitions';
import { IDisposable } from '@fluidframework/common-definitions';
import { IDocumentMessage } from '@fluidframework/protocol-definitions';
import { IDocumentStorageService } from '@fluidframework/driver-definitions';
import { IErrorEvent } from '@fluidframework/common-definitions';
import { IEvent } from '@fluidframework/common-definitions';
import { IEventProvider } from '@fluidframework/common-definitions';
import { IFluidCodeDetails } from '@fluidframework/core-interfaces';
import { IFluidConfiguration } from '@fluidframework/core-interfaces';
import { IFluidObject } from '@fluidframework/core-interfaces';
import { IFluidPackage } from '@fluidframework/core-interfaces';
import { IFluidPackageEnvironment } from '@fluidframework/core-interfaces';
import { IFluidResolvedUrl } from '@fluidframework/driver-definitions';
import { IFluidRouter } from '@fluidframework/core-interfaces';
import { IPendingProposal } from '@fluidframework/protocol-definitions';
import { IProvideFluidCodeDetailsComparer } from '@fluidframework/core-interfaces';
import { IQuorum } from '@fluidframework/protocol-definitions';
import { IRequest } from '@fluidframework/core-interfaces';
import { IResolvedUrl } from '@fluidframework/driver-definitions';
import { IResponse } from '@fluidframework/core-interfaces';
import { ISequencedDocumentMessage } from '@fluidframework/protocol-definitions';
import { ISignalClient } from '@fluidframework/protocol-definitions';
import { ISignalMessage } from '@fluidframework/protocol-definitions';
import { ISnapshotTree } from '@fluidframework/protocol-definitions';
import { ISummaryTree } from '@fluidframework/protocol-definitions';
import { ITelemetryBaseLogger } from '@fluidframework/common-definitions';
import { ITokenClaims } from '@fluidframework/protocol-definitions';
import { ITree } from '@fluidframework/protocol-definitions';
import { IVersion } from '@fluidframework/protocol-definitions';
import { MessageType } from '@fluidframework/protocol-definitions';

// @public (undocumented)
export enum AttachState {
    // (undocumented)
    Attached = "Attached",
    // (undocumented)
    Attaching = "Attaching",
    // (undocumented)
    Detached = "Detached"
}

// @public (undocumented)
export enum BindState {
    // (undocumented)
    Binding = "Binding",
    // (undocumented)
    Bound = "Bound",
    // (undocumented)
    NotBound = "NotBound"
}

// @public
export enum ContainerErrorType {
    dataCorruptionError = "dataCorruptionError",
    dataProcessingError = "dataProcessingError",
    genericError = "genericError",
    throttlingError = "throttlingError"
}

// @public
export interface ContainerWarning extends IErrorBase {
    logged?: boolean;
}

// @public
export interface IAudience extends EventEmitter {
    getMember(clientId: string): IClient | undefined;
    getMembers(): Map<string, IClient>;
    // (undocumented)
    on(event: "addMember" | "removeMember", listener: (clientId: string, client: IClient) => void): this;
}

// @public
export interface ICodeAllowList {
    // (undocumented)
    testSource(source: IResolvedFluidCodeDetails): Promise<boolean>;
}

// @public @deprecated
export interface ICodeLoader extends Partial<IProvideFluidCodeDetailsComparer> {
    load(source: IFluidCodeDetails): Promise<IFluidModule>;
}

// @public
export interface IConnectionDetails {
    checkpointSequenceNumber: number | undefined;
    // (undocumented)
    claims: ITokenClaims;
    // (undocumented)
    clientId: string;
    // (undocumented)
    existing: boolean;
    // (undocumented)
    initialClients: ISignalClient[];
    // (undocumented)
    maxMessageSize: number;
    // (undocumented)
    mode: ConnectionMode;
    // (undocumented)
    serviceConfiguration: IClientConfiguration;
    // (undocumented)
    version: string;
}

// @public
export interface IContainer extends IEventProvider<IContainerEvents>, IFluidRouter {
    attach(request: IRequest): Promise<void>;
    readonly attachState: AttachState;
    close(error?: ICriticalContainerError): void;
    closeAndGetPendingLocalState(): string;
    readonly closed: boolean;
    readonly codeDetails: IFluidCodeDetails | undefined;
    deltaManager: IDeltaManager<ISequencedDocumentMessage, IDocumentMessage>;
    getAbsoluteUrl(relativeUrl: string): Promise<string | undefined>;
    getQuorum(): IQuorum;
    readonly isDirty: boolean;
    proposeCodeDetails(codeDetails: IFluidCodeDetails): Promise<boolean>;
    request(request: IRequest): Promise<IResponse>;
    resolvedUrl: IResolvedUrl | undefined;
    serialize(): string;
}

// @public
export interface IContainerContext extends IDisposable {
    readonly attachState: AttachState;
    // (undocumented)
    readonly audience: IAudience | undefined;
    // (undocumented)
    readonly baseSnapshot: ISnapshotTree | undefined;
    // (undocumented)
    readonly clientDetails: IClientDetails;
    // (undocumented)
    readonly clientId: string | undefined;
    // (undocumented)
    readonly closeFn: (error?: ICriticalContainerError) => void;
    // (undocumented)
    readonly configuration: IFluidConfiguration;
    // (undocumented)
    readonly connected: boolean;
    // (undocumented)
    readonly deltaManager: IDeltaManager<ISequencedDocumentMessage, IDocumentMessage>;
    // (undocumented)
    readonly existing: boolean | undefined;
    getAbsoluteUrl?(relativeUrl: string): Promise<string | undefined>;
    // (undocumented)
    getLoadedFromVersion(): IVersion | undefined;
    // (undocumented)
    readonly id: string;
    // (undocumented)
    readonly loader: ILoader;
    // @deprecated (undocumented)
    readonly logger: ITelemetryBaseLogger;
    // (undocumented)
    readonly options: ILoaderOptions;
    // (undocumented)
    pendingLocalState?: unknown;
    // (undocumented)
    readonly quorum: IQuorum;
    // (undocumented)
    raiseContainerWarning(warning: ContainerWarning): void;
    readonly scope: IFluidObject;
    // (undocumented)
    readonly serviceConfiguration: IClientConfiguration | undefined;
    // (undocumented)
    readonly storage: IDocumentStorageService;
    // (undocumented)
    readonly submitFn: (type: MessageType, contents: any, batch: boolean, appData?: any) => number;
    // (undocumented)
    readonly submitSignalFn: (contents: any) => void;
    // (undocumented)
    readonly taggedLogger?: ITelemetryBaseLogger;
    // (undocumented)
    updateDirtyContainerState(dirty: boolean): void;
}

// @public
export interface IContainerEvents extends IEvent {
    // (undocumented)
    (event: "readonly", listener: (readonly: boolean) => void): void;
    // (undocumented)
    (event: "connected", listener: (clientId: string) => void): any;
    // (undocumented)
    (event: "codeDetailsProposed", listener: (codeDetails: IFluidCodeDetails, proposal: IPendingProposal) => void): any;
    // (undocumented)
    (event: "contextChanged", listener: (codeDetails: IFluidCodeDetails) => void): any;
    // (undocumented)
    (event: "disconnected" | "attached", listener: () => void): any;
    // (undocumented)
    (event: "closed", listener: (error?: ICriticalContainerError) => void): any;
    // (undocumented)
    (event: "warning", listener: (error: ContainerWarning) => void): any;
    // (undocumented)
    (event: "op", listener: (message: ISequencedDocumentMessage) => void): any;
    // (undocumented)
    (event: "dirty" | "saved", listener: (dirty: boolean) => void): any;
}

// @public (undocumented)
export interface IContainerLoadMode {
    // (undocumented)
    deltaConnection?: "none" | "delayed" | undefined;
    // (undocumented)
    opsBeforeReturn?: undefined | "cached" | "all";
}

// @public
export type ICriticalContainerError = IErrorBase;

// @public
export interface IDeltaHandlerStrategy {
    process: (message: ISequencedDocumentMessage) => void;
    processSignal: (message: ISignalMessage) => void;
}

// @public
export interface IDeltaManager<T, U> extends IEventProvider<IDeltaManagerEvents>, IDeltaSender, IDisposable {
    readonly active: boolean;
    readonly clientDetails: IClientDetails;
    close(): void;
    readonly hasCheckpointSequenceNumber: boolean;
    readonly inbound: IDeltaQueue<T>;
    readonly inboundSignal: IDeltaQueue<ISignalMessage>;
    readonly initialSequenceNumber: number;
    readonly lastKnownSeqNumber: number;
    readonly lastMessage: ISequencedDocumentMessage | undefined;
    readonly lastSequenceNumber: number;
    readonly maxMessageSize: number;
    readonly minimumSequenceNumber: number;
    readonly outbound: IDeltaQueue<U[]>;
    // @deprecated
    readonly readonly?: boolean;
    // (undocumented)
    readonly readOnlyInfo: ReadOnlyInfo;
    readonly serviceConfiguration: IClientConfiguration | undefined;
    submitSignal(content: any): void;
    readonly version: string;
}

// @public
export interface IDeltaManagerEvents extends IEvent {
    // (undocumented)
    (event: "prepareSend", listener: (messageBuffer: any[]) => void): any;
    // (undocumented)
    (event: "submitOp", listener: (message: IDocumentMessage) => void): any;
    // (undocumented)
    (event: "op", listener: (message: ISequencedDocumentMessage, processingTime: number) => void): any;
    // (undocumented)
    (event: "allSentOpsAckd", listener: () => void): any;
    // (undocumented)
    (event: "pong" | "processTime", listener: (latency: number) => void): any;
    (event: "connect", listener: (details: IConnectionDetails, opsBehind?: number) => void): any;
    // (undocumented)
    (event: "disconnect", listener: (reason: string) => void): any;
    // (undocumented)
    (event: "readonly", listener: (readonly: boolean) => void): any;
}

// @public
export interface IDeltaQueue<T> extends IEventProvider<IDeltaQueueEvents<T>>, IDisposable {
    idle: boolean;
    length: number;
    pause(): Promise<void>;
    paused: boolean;
    peek(): T | undefined;
    resume(): void;
    toArray(): T[];
    // (undocumented)
    waitTillProcessingDone(): Promise<void>;
}

// @public
export interface IDeltaQueueEvents<T> extends IErrorEvent {
    // (undocumented)
    (event: "push" | "op", listener: (task: T) => void): any;
    // (undocumented)
    (event: "idle", listener: (count: number, duration: number) => void): any;
}

// @public (undocumented)
export const IDeltaSender: keyof IProvideDeltaSender;

// @public
export interface IDeltaSender extends IProvideDeltaSender {
    flush(): void;
}

// @public
export interface IErrorBase {
    readonly errorType: string;
    // (undocumented)
    readonly message: string;
}

// @public
export interface IFluidBrowserPackage extends IFluidPackage {
    // (undocumented)
    fluid: {
        browser: IFluidBrowserPackageEnvironment;
        [environment: string]: IFluidPackageEnvironment;
    };
}

// @public
export interface IFluidBrowserPackageEnvironment extends IFluidPackageEnvironment {
    umd: {
        files: string[];
        library: string;
    };
}

// @public
export interface IFluidCodeResolver {
    resolveCodeDetails(details: IFluidCodeDetails): Promise<IResolvedFluidCodeDetails>;
}

// @public (undocumented)
export interface IFluidModule {
    // (undocumented)
    fluidExport: IFluidObject & Partial<Readonly<IProvideFluidCodeDetailsComparer>>;
}

// @public (undocumented)
export const IFluidTokenProvider: keyof IProvideFluidTokenProvider;

// @public (undocumented)
export interface IFluidTokenProvider extends IProvideFluidTokenProvider {
    // (undocumented)
    intelligence: {
        [service: string]: any;
    };
}

// @public
export interface IGenericError extends IErrorBase {
    // (undocumented)
    error?: any;
    // (undocumented)
    readonly errorType: ContainerErrorType.genericError;
}

// @public
export interface IHostLoader extends ILoader {
    createDetachedContainer(codeDetails: IFluidCodeDetails): Promise<IContainer>;
    rehydrateDetachedContainerFromSnapshot(snapshot: string): Promise<IContainer>;
}

// @public
export interface ILoader extends IFluidRouter {
    resolve(request: IRequest, pendingLocalState?: string): Promise<IContainer>;
}

// @public
export interface ILoaderHeader {
    // (undocumented)
    [LoaderHeader.cache]: boolean;
    // (undocumented)
    [LoaderHeader.clientDetails]: IClientDetails;
    // (undocumented)
    [LoaderHeader.reconnect]: boolean;
    // (undocumented)
    [LoaderHeader.sequenceNumber]: number;
    // (undocumented)
    [LoaderHeader.loadMode]: IContainerLoadMode;
    // (undocumented)
    [LoaderHeader.version]: string | undefined;
}

// @public (undocumented)
export type ILoaderOptions = {
    [key in string | number]: any;
} & {
    cache?: boolean;
    provideScopeLoader?: boolean;
    noopTimeFrequency?: number;
    noopCountFrequency?: number;
    maxClientLeaveWaitTime?: number;
};

// @public (undocumented)
export interface IPendingLocalState {
    // (undocumented)
    pendingRuntimeState: unknown;
    // (undocumented)
    url: string;
}

// @public (undocumented)
export interface IProvideDeltaSender {
    // (undocumented)
    readonly IDeltaSender: IDeltaSender;
}

// @public (undocumented)
export interface IProvideFluidTokenProvider {
    // (undocumented)
    readonly IFluidTokenProvider: IFluidTokenProvider;
}

// @public (undocumented)
export interface IProvideRuntimeFactory {
    // (undocumented)
    readonly IRuntimeFactory: IRuntimeFactory;
}

// @public
export interface IProxyLoaderFactory {
    createProxyLoader(id: string, options: ILoaderOptions, resolved: IFluidResolvedUrl, fromSequenceNumber: number): Promise<ILoader>;
    environment: string;
}

// @public
export interface IResolvedFluidCodeDetails extends IFluidCodeDetails {
    readonly resolvedPackage: Readonly<IFluidPackage>;
    readonly resolvedPackageCacheId: string | undefined;
}

// @public
export interface IRuntime extends IDisposable {
    // (undocumented)
    createSummary(): ISummaryTree;
    getPendingLocalState(): unknown;
    process(message: ISequencedDocumentMessage, local: boolean, context: any): any;
    processSignal(message: any, local: boolean): any;
    request(request: IRequest): Promise<IResponse>;
    setAttachState(attachState: AttachState.Attaching | AttachState.Attached): void;
    setConnectionState(connected: boolean, clientId?: string): any;
    snapshot(tagMessage: string, fullTree?: boolean): Promise<ITree | null>;
    // @deprecated (undocumented)
    stop(): Promise<{
        snapshot?: never;
        state?: never;
    }>;
}

// @public (undocumented)
export const IRuntimeFactory: keyof IProvideRuntimeFactory;

// @public
export interface IRuntimeFactory extends IProvideRuntimeFactory {
    instantiateRuntime(context: IContainerContext, existing?: boolean): Promise<IRuntime>;
}

// @public
export const isFluidBrowserPackage: (maybePkg: any) => maybePkg is Readonly<IFluidBrowserPackage>;

// @public
export interface IThrottlingWarning extends IErrorBase {
    // (undocumented)
    readonly errorType: ContainerErrorType.throttlingError;
    // (undocumented)
    readonly retryAfterSeconds: number;
}

// @public
export enum LoaderHeader {
    cache = "fluid-cache",
    // (undocumented)
    clientDetails = "fluid-client-details",
    loadMode = "loadMode",
    // (undocumented)
    reconnect = "fluid-reconnect",
    // (undocumented)
    sequenceNumber = "fluid-sequence-number",
    version = "version"
}

// @public (undocumented)
export type ReadOnlyInfo = {
    readonly readonly: false | undefined;
} | {
    readonly readonly: true;
    readonly forced: boolean;
    readonly permissions: boolean | undefined;
    readonly storageOnly: boolean;
};


// (No @packageDocumentation comment for this package)

```
